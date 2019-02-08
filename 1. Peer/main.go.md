```

import (
	_ "net/http/pprof"
	"os"
	"strings"

	"github.com/hyperledger/fabric/peer/chaincode"
	"github.com/hyperledger/fabric/peer/channel"
	"github.com/hyperledger/fabric/peer/clilogging"
	"github.com/hyperledger/fabric/peer/common"
	"github.com/hyperledger/fabric/peer/node"
	"github.com/hyperledger/fabric/peer/version"
	"github.com/spf13/cobra"
	"github.com/spf13/viper"
)

```

Making a peer command by cobra.
```
// The main command describes the service and
// defaults to printing the help message.
var mainCmd = &cobra.Command{
	Use: "peer"}
```

Setting configuration by viper
```
	// For environment variables.
	viper.SetEnvPrefix(common.CmdRoot)
	viper.AutomaticEnv()
	replacer := strings.NewReplacer(".", "_")
	viper.SetEnvKeyReplacer(replacer)
```
Setting cobra and viper logging level
```
	mainFlags := mainCmd.PersistentFlags()

	mainFlags.String("logging-level", "", "Legacy logging level flag")
	viper.BindPFlag("logging_level", mainFlags.Lookup("logging-level"))
	mainFlags.MarkHidden("logging-level")
```

Adding each additional commands to peer command
```
	mainCmd.AddCommand(version.Cmd())
	mainCmd.AddCommand(node.Cmd())
	mainCmd.AddCommand(chaincode.Cmd(nil))
	mainCmd.AddCommand(clilogging.Cmd(nil))
	mainCmd.AddCommand(channel.Cmd(nil))
```
execution
```
	// On failure Cobra prints the usage message and error string, so we only
	// need to exit with a non-0 status
	if mainCmd.Execute() != nil {
		os.Exit(1)
	}
  ```
