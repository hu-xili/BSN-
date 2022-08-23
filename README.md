# BSN-
使用BSN提供的go-SDK包连接测试网并调用链码
1、config.json文件
(注意：config.json文件放置位置要与main.go在同一文件夹，即：例如某一个name.go文件引用了bsnlink内的函数，config.json文件要和 name.go文件在同一文件夹内)
BSN网关api改变时更改json文件，'api','userCode','appCode'，在BSN上部署链码后会自动生成，而且生成BsnTestnetCert(测试网)证书文件，'privateKey','publicKey'，为生成的证书文件中用户证书对应的公私钥，'chainCode'，为链码部署名称。

2、对NFT区块对象的函数使用方法（即：将NFT区块状态记录到BSN上的增删改查以及查询历史记录相关）
init()
功能：初始化从配置文件读取config，函数运行时自动读取，不用修改

func GenClient() *fabric.FabricClient
产生FabricClient，进行下一步操作，不用修改，已经封装到后续所有函数内部，管理人员知道有这个函数就行

func Set(block NFTBlockState)
功能：将区块链状态对象记录到BSN链上。 输入：NFTBlockState结构体，结构体中BlockHash（区块哈希）为必填的值。 用法：将获取到的区块信息构建成NFTBlockState结构体输入即可。

func Query(hash string)
功能：根据NFT链上的区块哈希查询其被记录在BSN上的信息。 输入：NFT链上的区块哈希。

func Update(block NFTBlockState)
功能：更新记录的区块状态信息。 用法：同上面的Set函数相同。

func Delete(hash string)
功能：根据NFT链上的区块哈希删除其被记录在BSN上的信息。 用法：同上面Query函数相同。

func QueryHistory(hash string)
功能：根据NFT链上的区块哈希查询其被记录在BSN上的历史信息，即使已经被删除也能查询到。

3、对BSN链上区块的一些操作
func GetTransInfo(txId string)
功能：根据在bsn上产生的交易id查询交易信息。 用法：输入交易产生的交易id。

func GetTransDataInfo(txId string)
功能：根据在bsn上产生的交易id查询交易数据信息。 用法：输入交易产生的交易id。

func GetBlockInfo(height uint64)
功能：获取BSN上指定区块高度的区块信息。 用法：直接输入想要查询的区块高度。

func GetBlockDataInfo(txId string)
功能：根据在bsn上产生的交易id查询交易参与出块的区块数据信息。 用法：输入交易产生的交易id。

func GetLedgerInfo()
功能：获取账本信息。 用法：直接使用，无需输入参数。
