# Practice-basic-AWS

#search and install aws cli, type in terminal instead of gitpod
#curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg" (for Macbook)
#sudo installer -pkg AWSCLIV2.pkg -target /
#which aws
aws --version

#"cd /workspace", "sudo ./aws/install", "cd /workspace/AWS-Examples", "cd THEIA_WORKSPACE_ROOT" and "env | grep AWS-Example" what are these? should I need to use or not? 

#這些命令主要用於在特定的工作環境中操作，通常是在使用 Gitpod 或類似的在線 IDE 時。以下是每個命令的解釋：

cd /workspace:

這個命令將當前目錄更改為 /workspace，這是 Gitpod 等在線 IDE 中的默認工作目錄。
sudo ./aws/install:

這個命令通常用於安裝 AWS CLI。它在當前目錄下運行 aws 資料夾中的安裝腳本，使用 sudo 提升權限。
cd /workspace/AWS-Examples:

這個命令將當前目錄更改為 /workspace/AWS-Examples，通常是一個示例項目或資料夾，可能包含 AWS 的使用示例。
cd THEIA_WORKSPACE_ROOT:

這個命令用於更改目錄到 Theia 工作空間的根目錄。Theia 是一種開源的 IDE，類似於 VS Code。
env | grep AWS-Example:

這個命令用於查看當前環境變數中是否包含與 AWS-Example 相關的內容。env 命令列出所有環境變數，grep 用於過濾結果。
是否需要使用？

如果你是在 Gitpod 或類似的環境中工作，並且需要安裝 AWS CLI 或進入特定的工作目錄，那麼這些命令可能會很有用。
如果你只是想在本地機器上使用 AWS CLI，那麼這些命令可能不需要。
根據你的具體工作流程，決定是否使用這些命令。

#login to aws
#Search bar => type 'iam' => select 'IAM' => select 'Users' => select 'Create user' => type 'aws-examples' in User name => click 'Next' => Permissions options is 'Add user to group' => Group name select 'Admin' => click 'Next' => click 'Create user' 

#after create user, click ''aws-examples' => select 'Security credentials' to generate credential => select 'Create access key' => select 'Command Line Interface (CLI) => click 'Next' => click 'Create access key'

#search 'aw