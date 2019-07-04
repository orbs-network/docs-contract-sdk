# Limitations of Orbs Contracts

Orbs contracts are written in the Go programming language.

To enhance the security and enable multiple virtual chains in the Orbs blockchain, the smart contracts are limited in regards of the Go language. Specifically, which features and packages of the language are allowed to execute inside the Orbs Virtual Machine.

### Package Whitelist

All packages in Go are not allowed with the exception of specific packages expressed in the whitelist below:

```text
// Orbs Contract SDK
"github.com/orbs-network/orbs-contract-sdk/go/sdk/v1"
"github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/address"
"github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/env"
"github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/ethereum"
"github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/events"
"github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/safemath"
"github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/safemath/safeuint32"
"github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/safemath/safeuint64"
"github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/safemath/safeuint256"
"github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/service"
"github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/state"

// Text
"strings"
"strconv"
"text/template"

// Time
"time"

// Binary
"bytes"
"encoding/binary"
"io"

// Encoding
"encoding/json"
"encoding/hex"
"encoding/base32"
"encoding/base64"

// Utils
"sort"
```

Trying to include any package **not** in that list will result failed compilation of the smart contract.

### Time functions blacklist

While we enable the use of the time package for time manipulation, it contains several functions which would result inconsistent and non-deterministic results in contracts, and thus they are blacklisted, these functions are:

```text
"After"
"AfterFunc"
"Sleep"
"Tick"
"NewTimer"
"NewTicker"
"Now"
```

Using any of these functions will result failed compilation of the smart contract.

{% hint style="info" %}
If you want the current time \('Now'\), it is possible to use the contract SDK function `env.GetBlockTimestamp()` 
{% endhint %}

### Blacklisted Features

Aside from a whitelist of the allowed packages, Orbs will not allow the usage of the following Go language features:

* Channels
* Goroutines \(the `go` statement\)
* The 'arrow' unary expression \(`<-`\)

Using any of the above will result in a failed compilation of the smart contract.

