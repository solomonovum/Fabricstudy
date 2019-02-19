
```
import (
	"fmt"

	"github.com/hyperledger/fabric/common/flogging" // logger
	"github.com/hyperledger/fabric/peer/common"
	"github.com/spf13/cobra"
)
```

For cobra setting
```
const (
	nodeFuncName = "node"
	nodeCmdDes   = "Operate a peer node: start|status."
)
```

Creation of logger
```
var logger = flogging.MustGetLogger("nodeCmd")
```

Adding start, status commands to node
```
// Cmd returns the cobra command for Node
func Cmd() *cobra.Command {
	nodeCmd.AddCommand(startCmd())
	nodeCmd.AddCommand(statusCmd())

	return nodeCmd
}
```

Making a node command.
```
var nodeCmd = &cobra.Command{
	Use:              nodeFuncName,
	Short:            fmt.Sprint(nodeCmdDes),
	Long:             fmt.Sprint(nodeCmdDes),
	PersistentPreRun: common.InitCmd,
}
```
