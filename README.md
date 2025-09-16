# Practice-basic-AWS
#Only the README.md has information and includes the steps to install the AWS CLI and use basic AWS services. Thanks

#Reference: https://youtu.be/c3Cn4xYfxJY?si=m4LpdAaeJxxCJxVY 
#search and install aws cli, type in terminal instead of using gitpod
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

#search 'aws env vars' => click 'Environment variables to configure the AWS CLI' 
#"Configuring environment variables for the AWS CLI." What is it? Should I need to configure it or not if I use git and AWS IAM? 

#“配置 AWS CLI 的環境變數”是指設置一些變數，使得 AWS CLI 可以正確運行並訪問你的 AWS 賬戶。這些環境變數通常包括你的 AWS 訪問金鑰、秘密金鑰和所需的區域等信息。

需要配置的內容：
AWS_ACCESS_KEY_ID: 你的 AWS 訪問金鑰 ID。
AWS_SECRET_ACCESS_KEY: 你的 AWS 秘密金鑰。
AWS_DEFAULT_REGION: 你希望使用的 AWS 區域（例如 us-east-1）。
是否需要配置？

如果你在使用 Git 和 AWS IAM:

是的，你需要配置環境變數或使用 aws configure 命令來設置這些參數。這樣 AWS CLI 才能夠識別你的身份並授權你訪問 AWS 服務。
如果你不配置:

AWS CLI 將無法正確運行，並且會出現授權錯誤。
總結

根據你的工作需求，正確配置 AWS CLI 的環境變數是必要的，這樣才能確保你能夠順利使用 AWS 的各項功能。

#"Setting the environment variable changes the value used until the end of your shell session, or until you set the variable to a different value. You can make the variables persistent across future sessions by setting them in your shell's startup script." What does that mean? Is it related to "Configuring environment variables for the AWS CLI"? 

#這段話的意思是：

環境變數的作用範圍：當你設置了一個環境變數後，這個變數的值將在當前的 shell 會話中有效，直到你關閉終端或將變數更改為其他值。

持久化設置：如果你希望這些環境變數在未來的 shell 會話中仍然有效，你需要將它們設置在你的 shell 啟動腳本中。這樣，每次打開新的終端時，這些變數都會自動被設置。

與 AWS CLI 的關係

這與「配置 AWS CLI 的環境變數」是有關的，因為：

臨時設置：如果你只是臨時設置 AWS CLI 的環境變數，那麼在當前會話中它們會有效，但關閉終端後就會失效。

持久化設置：如果你將 AWS CLI 的環境變數添加到你的 shell 啟動腳本（例如 .bashrc 或 .zshrc），那麼每次你打開一個新的終端時，這些變數都會自動被設置，方便你隨時使用 AWS CLI。

總結

如果你經常使用 AWS CLI，建議將環境變數持久化設置，以便在每次啟動終端時自動配置，這樣可以提高工作效率。

#export AWS_ACCESS_KEY_ID=xxxxxxxxxxx
#export AWS_SECRET_ACCESS_KEY=xxxxxxxxxxx
#export AWS_REGION=xxxxxxxx(change to your local region)
#aws sts get-caller-identity
#after typing, I can see:
{
    "UserId": "12345abcde",
    "Account": "33445566",
    "Arn": "arn:aws:iam::33445566:user/AWS-Examples"
}
#這段 JSON 格式的資料包含了有關 AWS IAM 使用者的信息，具體如下：

1."UserId": "12345abcde":
這是該使用者的唯一識別碼（User ID）。每個 IAM 使用者都有一個唯一的 ID，用於識別該使用者。

2."Account": "33445566":
這是與該使用者相關聯的 AWS 賬戶 ID。這個 ID 是 AWS 用戶的識別碼，通常用於管理和計費。

3."Arn": "arn:aws:iam::33445566:user/AWS-Examples":
這是該使用者的 Amazon 資源名稱（ARN，Amazon Resource Name）。ARN 是 AWS 中用來唯一標識資源的名稱。在這裡，它表示一個名為 AWS-Examples 的 IAM 使用者。

#總結:
這段 JSON 主要用於提供有關 AWS IAM 使用者的基本信息，包括其唯一識別碼、所屬賬戶 ID 以及資源名稱。這些信息在 AWS 管理和安全性設定中非常重要。

=====================================================================================
====================================================================================
=====================================================================================

#aws s3 ls
#Error: An error occurred (AccessDenied) when calling the ListBuckets operation: 
#search 'aws cli credentials file' => click 'Configuration and credential file settings in the AWS CLI' 

錯誤信息顯示你的 AWS IAM 用戶沒有必要的權限來執行 s3:ListAllMyBuckets 操作。以下是解決此問題的步驟：

Reference: how to create s3 bucket https://www.google.com/search?q=create+a+s3+bucket&rlz=1C5CHFA_enHK983HK983&oq=create+a+s3&gs_lcrp=EgZjaHJvbWUqCQgBEAAYExiABDIGCAAQRRg5MgkIARAAGBMYgAQyCQgCEAAYExiABDIJCAMQABgTGIAEMgkIBBAAGBMYgAQyCAgFEAAYExgeMggIBhAAGBMYHjIICAcQABgTGB4yCAgIEAAYExgeMggICRAAGBMYHtIBCDQ5MzJqMGo3qAIAsAIA&sourceid=chrome&ie=UTF-8#fpstate=ive&vld=cid:50b7d962,vid:9gtOkz4Ybdg,st:0 

1. create s3 bucket => search 's3' in search bar => create s3 bucket. 
2. 附加策略

進入 IAM 控制台：

登錄到 AWS 管理控制台，然後打開 IAM 服務。
選擇用戶：

在左側邊欄中點擊「Users」。
選擇你的用戶：

點擊你正在使用的用戶（例如 AWS-Examples）。
附加策略：

轉到「Permissions」標籤。
點擊「Add permissions」，select'Add user to group' => click'create group' => enter 'User group name' and select 'permission policy' (e.g, 'AdministratorAccess: Info:
Provides full access to AWS services and resources') => click 'create user group' => user group created => 然後點擊「Add permissions」。

#aws s3 ls => output: 2029-10-10 03:10:10 aws-s3-AAAAAA

=====================================================================================
=======================================================================================================================================================================

#aws configure list => AWS CLI 配置：確保你的 AWS CLI 配置正確，使用了正確的訪問密鑰、秘密密鑰和區域。

#aws s3api list-buckets => 嘗試運行以下命令，查看是否可以獲取桶的信息

#search 's3' in my aws console => create bucket.
#以下是 Amazon S3 中不同伺服器端加密類型的詳細說明：

1. Server-side encryption with Amazon S3 managed keys (SSE-S3)
=> 使用 Amazon S3 管理的鍵進行的伺服器端加密 (SSE-S3)
#描述：
SSE-S3 使用 Amazon S3 管理的鍵來加密靜態數據。
每個對象使用唯一的加密密鑰，這些密鑰又用主密鑰進行加密。
Amazon S3 自動處理密鑰的創建、管理和銷毀。
#使用情況：
當你的數據不需要額外的密鑰管理或控制時，使用 SSE-S3 是一個簡單且安全的選擇。
適合大多數用例，特別是對於不需要合規性或審計要求的數據。

2. Server-side encryption with AWS Key Management Service keys (SSE-KMS)
=> 使用 AWS 密鑰管理服務鍵進行的伺服器端加密 (SSE-KMS)
#描述：
SSE-KMS 使用 AWS Key Management Service (KMS) 來管理加密密鑰。
這允許更細粒度的控制，包括密鑰的創建、管理和使用權限。
可以設置 IAM 政策來控制誰可以使用密鑰。
#使用情況：
當你需要嚴格的密鑰管理和細粒度訪問控制時，使用 SSE-KMS 是合適的選擇。
當 data compliance（數據合規性）和審計要求提高時，這是一個理想的選擇，例如金融、醫療或法律領域。

3. Dual-layer server-side encryption with AWS Key Management Service keys (DSSE-KMS)=> 使用 AWS 密鑰管理服務鍵的雙層伺服器端加密 (DSSE-KMS)
=> 依個encryption要俾錢
#描述：
DSSE-KMS 提供了雙層加密，將數據首先使用 SSE-KMS 加密，然後再使用另一個密鑰進行加密。
這種方法進一步增強了數據的安全性，適合需要更高層級保護的業務需求。
#使用情況：
當數據特別敏感，並且需要額外的安全層時，使用 DSSE-KMS 是合適的選擇。
適合需要最高級別安全性的應用場景，如政府機構或涉及敏感個人數據的企業。
#總結:
選擇適合的加密類型取決於你的業務需求、合規要求以及數據敏感性。對於一般用途，SSE-S3 已足夠；對於需要更高安全性和控制的情況，SSE-KMS 和 DSSE-KMS 是更合適的選擇。
#https://aws.amazon.com/tw/s3/pricing/ => including the price of encryption types

==================================================================================
==================================================================================

#以下是有關 Amazon S3 中物件鎖定 (Object Lock) 的使用情況以及何時選擇啟用或禁用的建議：

物件鎖定 (Object Lock) 的概述

物件鎖定提供了一種寫一次讀多次 (WORM) 模型，幫助防止對象在固定時間內或無限期內被刪除或覆蓋。物件鎖定僅在版本化的桶中有效。

#啟用物件鎖定的情況 (enable object lock)
1.合規性要求：(enable object lock)
如果你的行業或業務需要遵循合規性法規（例如金融或醫療），必須保存數據且不能隨意刪除，則應啟用物件鎖定。
2.數據保護：(enable object lock)
當你需要防止意外刪除或覆蓋重要數據時，例如關鍵的業務記錄或法律文件，啟用物件鎖定可以提供額外的安全層。
3.長期存儲：(enable object lock)
如果數據需要長期保存，並且在此期間不應被修改或刪除，則應選擇啟用物件鎖定。

#禁用物件鎖定的情況(disable object lock)
1.靈活性需求：(disable object lock)
如果你的業務需要靈活地刪除或更新數據，則應考慮禁用物件鎖定。這樣，你可以隨時管理和清理數據。
2.非關鍵數據：(disable object lock)
對於不那麼重要或不需要長期保存的數據，禁用物件鎖定可能更合適，因為這樣可以減少管理複雜性。
3.測試或開發：(disable object lock)
在開發或測試環境中，通常需要更改或刪除數據，因此在這些情況下禁用物件鎖定是合理的。

#總結:
選擇啟用或禁用物件鎖定取決於你的業務需求和數據管理策略。如果你需要強化數據保護和合規性，則應啟用物件鎖定；如果需要靈活性和簡化管理，則可以選擇禁用。

#"Configuring environment variables for the AWS CLI."

#什麼是桶策略（Bucket Policy）？

桶策略是一種基於資源的訪問策略，使用 JSON 格式編寫，旨在控制對 Amazon S3 桶及其內容的訪問。它允許你定義誰可以訪問桶中的對象、可以執行哪些操作（如讀取或寫入對象）以及在什麼條件下可以執行這些操作。

桶策略的功能

訪問控制：決定哪些用戶或角色可以訪問桶中的對象。
條件限制：可以基於 IP 地址、請求時間等條件限制訪問。
允許或拒絕操作：可以明確允許或拒絕特定的 S3 操作。
桶策略示例

以下是一些常見的桶策略示例：

1. 允許所有人讀取桶中的對象
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::your-bucket-name/*"
        }
    ]
}
此策略允許任何人（Principal: "*"）讀取指定桶中的所有對象。

2. 僅允許特定 AWS 帳戶訪問
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::123456789012:root"
            },
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::your-bucket-name"
        }
    ]
}
3. 限制訪問僅允許特定 IP 地址
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::your-bucket-name/*",
            "Condition": {
                "IpAddress": {
                    "aws:SourceIp": "200.0.111.0/24"
                }
            }
        }
    ]
}
此策略僅允許來自特定 IP 地址範圍的請求讀取桶中的對象。

=====================================================================================
====================================================================================
=====================================================================================

以下是s3 bucket policy 的逐行解釋：
In bucket policy=> can see Bucket ARN => arn:aws:s3:::aws-s3-AAAAA (copy and paste)
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::aws-s3-AAAAA/*"
        }
    ]
}


1. "Version": "2012-10-17"
=> 在這裡，使用的是 2012 年 10 月 17 日的版本，這是 AWS 策略語法的標準版本。

2. "Effect": "Allow"
=> 在這裡，"Allow" 表示允許指定的操作。

3. "Principal": "*"
=> 指定這個policy適用的主體（Principal）。"*" 表示所有用戶和角色都可以適用這個policy，即任何人都可以訪問。

4. "Action": "s3:GetObject"
=> 在這裡，"s3:GetObject" 表示允許用戶從 S3 桶中獲取對象（即下載文件）。

5. "Resource": "arn:aws:s3:::aws-s3-AAAAA/*"
=> 在這裡，arn:aws:s3:::aws-s3-AAAAA/* 表示這個policy適用於 aws-s3-AAAAA 桶中的所有對象。
=> /* 表示bucket中的所有文件。

#Summary: 這段策略的作用是允許所有用戶從名為 aws-s3-AAAAA 的 S3 桶中獲取對象，這意味著任何人都可以下載桶中的文件。這樣的策略通常用於需要公開訪問的資料。

=====================================================================================
====================================================================================
=====================================================================================

What is a 'Bucket ARN' (e.g, arn:aws:s3:::aws-s3-AAAAA/*)?

ARN stands for 'Amazon Resource Name', which is a 'unique identifier' for 'AWS resources'. A Bucket ARN specifically identifies an Amazon S3 bucket.

#The format of a Bucket ARN is:
#arn:aws:s3:::bucket-name

1. arn: The prefix for all ARN identifiers.
2. aws: Indicates that this resource is part of AWS.
3. s3: Specifies that the resource is an Amazon S3 bucket.
4. bucket-name: The name of your S3 bucket.

#Example: For a bucket named my-example-bucket, the ARN would be:
#arn:aws:s3:::my-example-bucket

#Use Cases:
1. IAM Policies: Bucket ARNs are used in IAM policies to specify permissions for accessing or managing the bucket.

2. Bucket Policies: You can use Bucket ARNs in bucket policies to control access to the bucket and its contents.

3. Logging and Monitoring: ARNs can be referenced in logging and monitoring services to track actions related to specific buckets.

#Summary: A Bucket ARN uniquely identifies an S3 bucket within AWS, allowing you to manage permissions and access controls effectively.


#aws --version => Ensure you have the AWS CLI installed. You can check by running.
#aws configure =>  Make sure you've configured it with your credentials. 


#List Files in an S3 Bucket: To see the files in a specific S3 bucket:
#aws s3 ls s3://your-bucket-name/ (e.g, aws s3 ls s3://aws-s3-AAAAA/)

#Download a File from an S3 Bucket: To download a specific file from the S3 bucket
#aws s3 cp s3://your-bucket-name/your-file-name local-file-name
1. your-bucket-name: The name of your S3 bucket.
2. your-file-name: The name of the file you want to download.
3. local-file-name: The name you want to give the downloaded file on your local machine (optional).

For example:
If s3 Bucket name:aws-s3-AAAAA Object name: IMAGE 2025-10-10 11:11:11.jpg
#aws s3 cp s3://aws-s3-AAAAA/"IMAGE 2025-10-10 11:11:11.jpg" "local-filename.jpg"
#output 'dowload'

#open local-filename.jpg => open jpg
#if you want to delete the jpg in aws:
#aws s3 rm s3://aws-s3-AAAAA/"IMAGE 2025-10-10 11:11:11.jpg" 
=> reload aws page, the system prompt 'The object "IMAGE 2025-09-11 17:48:25.jpg" was not found.' => deleted 

#If you want to delete 啱先download咗嘅jpg, dowload 咗嘅jpg轉左名local-filename.jpg
#rm local-filename.jpg => 咁就可以係自己部電腦刪除個jpg