# NEAR-STAKEWARS3-h-ng-d-n
Bài viết hướng dẫn trở thành validator trên mạng Shardnet của Near Protocol

Tôi có 1 video tổng quan bạn có thể tham khảo: https://youtu.be/npGqxKXJ3Nc
**Để tiến hành bạn cần có: 1 VPS linux, 1 tài khoản Shardnet, tài liệu Stake wars 3**

1. Tạo VPS
 Bạn có thể tạo vps bằng pc của bạn nhưng tôi khuyến nghị bạn nên thuê dịch vụ VPS để đảm bảo VPS của bạn luôn chạy ổn định. 
Có rất nhiều nhà cung cấp VPS, tôi đề xuất bạn sử dụng Hetzner với ưu điểm về hiệu năng trên giá thành tuyệt vời
Bạn cần đăng ký và KYC tài khoản của bạn để có thể thuê VPS
Sau đó tiến hành tạo 1 project trên Hetznet
![2022-09-05](https://user-images.githubusercontent.com/112862622/188422641-76e3b335-9dba-4aea-96f0-82363b73a53c.png)
![2022-09-05 (1)](https://user-images.githubusercontent.com/112862622/188422813-5f39e0e1-755f-41bb-ad6c-0fbaffb79618.png)
![2022-09-05 (2)](https://user-images.githubusercontent.com/112862622/188422904-537cfdd0-f601-4eeb-a1eb-787e9e63b0bb.png)
![2022-09-05 (3)](https://user-images.githubusercontent.com/112862622/188422932-9c02c931-d7eb-4ca6-b596-fdd261e25723.png)
![2022-09-05 (4)](https://user-images.githubusercontent.com/112862622/188422968-fe1af85c-ec34-4995-ab22-768b5ac432d9.png)
**Lưu ý: Cấu hình đề xuất của team near là 500GB SSD vì vậy bạn có thể sẽ cần mua thêm dung lượng. Cấu hình như hình trên là đủ để bạn bắt đầu
![image](https://user-images.githubusercontent.com/112862622/188423520-5d886c8e-266d-4c80-8141-ad3ba489485c.png)


2. Tạo tài khoản shardnet


Truy cập: https://wallet.shardnet.near.org/ để tạo tài khoản
![image](https://user-images.githubusercontent.com/112862622/188423843-562f954f-2096-410c-b771-19bac16db5be.png)
![image](https://user-images.githubusercontent.com/112862622/188423948-ffdd78e2-a3b1-4f0d-9e4d-1eb042c0b300.png)
Lưu ý: hãy lưu và cất giữ 12 cụm từ khi tạo tài khoản cẩn thận. Tôi nghĩ chúng ta có thể dùng tài khoản này khi mainnet và sẽ có nhiều điều tuyệt vời ở mạng Shardnet


3. Tài liệu Stake Wars 3;
Link: https://github.com/near/stakewars-iii

Đường dẫn trên sẽ bao gồm các thử thách và phần thưởng mỗi thử thách. Các thử thách chính là các bước với hướng dẫn để tạo và quản trị validators

**Các hướng dẫn ở các hướng dẫn đều rất chi tiết vì vậy tôi sẽ chỉ chụp lại những bước nếu cần thiết**

1. Thử thách 1 (challenges 1)

- Đầu tiên, hãy cập  nhật Linux cho vps của bạn
sudo apt update && sudo apt upgrade -y

- Cài đặt dev tool, Node.js và npm

    curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -  
    sudo apt install build-essential nodejs
    PATH="$PATH"

- Cài đặt NEAR-CLI

    sudo npm install -g near-cli

- Chọn mạng Shardnet cho Validator

export NEAR_ENV=shardnet

--- Một số câu lệnh giúp bạn xem danh sách các validator

- Các node đã được chấp thuận, các node này sẽ được tham gia xác thực nếu đủ lượng near trong pool

    near proposals

- Danh sách các validator hiện tại

    near validators current

- Các node đủ lượng near tối thiểu và chuẩn bị trở thành validator

near validators next

2. Thử thách 2 (challenges 2)
Khởi tạo 1 node(nearcore), tải về snapshot, syncing.

- Kiểm tra xem CPU VPS của bạn có hỗ trợ hay không:

      lscpu | grep -P '(?=.*avx )(?=.*sse4.2 )(?=.*cx16 )(?=.*popcnt )' > /dev/null \
      && echo "Supported" \
      || echo "Not supported"

- Tải và cài đặt dev tool

sudo apt install -y git binutils-dev libcurl4-openssl-dev zlib1g-dev libdw-dev libiberty-dev cmake gcc g++ python3 docker.io protobuf-compiler libssl-dev pkg-config clang llvm cargo

-Cài đặt Python pip

    sudo apt install python3-pip

-Đặt cấu hình

    USER_BASE_BIN=$(python3 -m site --user-base)/bin
    export PATH="$USER_BASE_BIN:$PATH"

- Cài Building env

sudo apt install clang build-essential make

Cài đặt Rust & Cargo

    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

- Khi cài sẽ có 3 lựa chọn hãy chọn mục 1

![2022-09-04 (12)](https://user-images.githubusercontent.com/112862622/188436045-e99647b8-5a79-41f3-9899-ef7e3ddd3483.png)

Source

    source $HOME/.cargo/env

- Sao chép nearcore từ Github

    git clone https://github.com/near/nearcore
    cd nearcore
    git fetch

![2022-09-04 (15)](https://user-images.githubusercontent.com/112862622/188436309-5f3c592c-70a9-4feb-9035-dcd6d218c17d.png)


- Checkout commit. Hãy đảm bảo bạn cài commit mới nhất tại https://github.com/near/stakewars-iii/blob/main/commit.md  thay <commit> bằng commit trong đường dẫn
Bạn có thể xem ví dụ ở hình phía trên

      git checkout <commit>

- Compile nearcore binary
  
  
        cargo build -p neard --release --features shardnet
  
  Bước này sẽ tốn chút thời gian, hãy nghỉ 1 chút và đợi nhé
  
  - Initialize working directory
  
       ./target/release/neard --home ~/.near init --chain-id shardnet --download-genesis
 - Khởi chạy Node
  
  Bước này node sẽ tải snapshot về sẽ tốn thời gian, vì vậy mình sẽ sử dụng tmux để chạy. Trong khi chờ mình có thể thực hiện các bước khác  (bạn có thể chạy mà không cần tmux cũng được). Xem hướng dẫn dùng tmux tại đây: https://www.hostinger.vn/huong-dan/tmux
  
  
    sudo apt install tmux
    tmux
    cd ~/nearcore
    ./target/release/neard --home ~/.near run
  Dùng Ctrl B + D để đóng tmux
  
  - Đăng nhập node vào ví Shardnet 
  
      near login
 Bạn sẽ nhận được 1 đường link, copy đường link đó vào trình duyệt chứa ví shardnet
  ![2022-09-05 (8)](https://user-images.githubusercontent.com/112862622/188439917-70078dda-4778-49d8-8ada-676b3e470aed.png)
![image](https://user-images.githubusercontent.com/112862622/188439967-34750ac2-476e-4312-9f6f-7a6d85f20562.png)
![image](https://user-images.githubusercontent.com/112862622/188440011-06b1bc97-2eec-42d5-85ec-baf09f84c64c.png)
![image](https://user-images.githubusercontent.com/112862622/188440085-fbe0d058-c3aa-45c5-b88e-1e7aa8d3fc27.png)
![image](https://user-images.githubusercontent.com/112862622/188440171-fbaec3b9-50bf-4447-b0a4-3f4b2c54db15.png)
Nếu có lỗi kết nối như hình trên là bình thường nhé
 Nhập địa chỉ ví của bạn để kiểm tra.
  ![image](https://user-images.githubusercontent.com/112862622/188440311-72e6c4f7-4683-4088-abf1-c6c51da37d3e.png)

- Kiểm tra validator_key.json của bạn
  
      cat ~/.near/validator_key.json
  
  Nếu không có hãy tạo 1 lệnh sinh key
  
      near generate-key <pool_id>
  
  Thay <pool_id> bằng tên đầu địa chỉ ví của bạn + .factory.shardnet.near
  
  Ví dụ: của tôi là bnb.factory.shardnet.near
  
- Copy địa chỉ ví của bạn  vào thư mục .near
  
      cp ~/.near-credentials/shardnet/YOUR_WALLET.json ~/.near/validator_key.json
- Chỉnh sửa file validator_key.json
  
     sudo nano .near/validator_key.json
  Đổi account_id thành xxx.factory.shardnet.near
File sau đó có dạng
  
{
    "account_id": "xx.factory.shardnet.near",
   "public_key": "ed25519:HeaBJ3xLgvZacQWmEctTeUqyfSU4SDEnEwckWxd92W2G",
   "secret_key": "ed25519:****"
 }
  - Kiểm tra tmux xem node đã tải về dữ liệu xong chưa
  Để xem gõ : 
      tmux attach-session -t 0
  Nếu đã xong, ta thoát ra kill tmux session đó đi
  Kill session 
      tmux kill-session -t 0
  - Khởi chạy validator node
      target/release/neard run
  
 - Tạo file service
      sudo nano /etc/systemd/system/neard.service
  Chỉnh sửa phần dưới đây và dán vào file. đổi theo user vps của bạn
        [Unit]
        Description=NEARd Daemon Service

        [Service]
        Type=simple
        User=<USER>
        #Group=near
        WorkingDirectory=/home/<USER>/.near
        ExecStart=/home/<USER>/nearcore/target/release/neard run
        Restart=on-failure
        RestartSec=30
        KillSignal=SIGINT
        TimeoutStopSec=45
        KillMode=mixed

        [Install]
        WantedBy=multi-user.target
  
- Bật service neard
  
      sudo systemctl enable neard
  
- Khởi động service neard
  
      sudo systemctl start neard
-Nếu có lỗi hãy thử chạy lại 
  
     sudo systemctl restart neard
 - Xem log
      journalctl -n 100 -f -u neard
 - Cài đặt màu cho log
        sudo apt install ccze
 - xem log có màu
        journalctl -n 100 -f -u neard | ccze -A
 
4. Thử thách 3 (challenges 3)
  
  Ghi chú:
  Pool Name: Tên Stacking pool. Nếu pool ID của bạn là Stakewars thì pool name là stakewars.factory.shardnet.near
  
  Owner ID: địa chỉ ví shardnet 
  Public key: Xem trong file validator_key.json
  Account ID: Địa chỉ ví dùng để ký giao dịch thường là Owner ID
  
  - Tạo 1 hợp đồng Staking pool
        
            near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "<pool name>", "owner_id": "<accountId>", "stake_public_key": "<public key>", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="<accountId>" --amount=30 --gas=300000000000000
  
 - Gửi near vào pool stake
  
        near call <pool_id> deposit_and_stake --amount <amount> --accountId <accountId> --gas=300000000000000
  
  - Unstake
  
        near call <pool_id> unstake '{"amount": "<amount yoctoNEAR>"}' --accountId <accountId> --gas=300000000000000
  
  - Rút
  
        near call <pool_id> withdraw '{"amount": "<amount yoctoNEAR>"}' --accountId <accountId> --gas=300000000000000
  - Rút toàn bộ
        near call <pool_id> withdraw_all --accountId <accountId> --gas=300000000000000
  
  - Ping
   
        near call <pool_id> ping '{}' --accountId <accountId> --gas=300000000000000
  Một ping đưa ra một đề xuất mới và cập nhật số dư đặt cược cho người ủy quyền của bạn. Một ping nên được phát hành mỗi kỷ nguyên để cập nhật phần thưởng được báo cáo.
  
  - Kiểm tra số dư stake trong pool
      
        near view <pool_id> get_account_staked_balance '{"account_id": "<accountId>"}'
  
  - Kiểm tra lượng near đã được unstake  
  
        near view <pool_id> get_account_staked_balance '{"account_id": "<accountId>"}'
  
  - Kiểm tra số near có thể rút
  
        near view <pool_id> is_account_unstaked_balance_available '{"account_id": "<accountId>"}'
  
  - Dừng/ tiếp tục staking
  
    Dừng
        near call <pool_id> pause_staking '{}' --accountId <accountId>
    Tiếp tục
        near call <pool_id> resume_staking '{}' --accountId <accountId>
        
5. Thử thách 4 (challenges 4)

  Cài đặt các công cụ để kiểm tra trạng thái node của bạn
  
 - Kiểm tra log 
        journalctl -n 100 -f -u neard | ccze -A
 - RPC
  
        sudo apt install curl jq
 - Kiểm tra phiên bản node của bạn
  
        curl -s http://127.0.0.1:3030/status | jq .version
  
  - Kiểm tra lượng stake của 1 delegator
  
        near view <your pool>.factory.shardnet.near get_accounts '{"from_index": 0, "limit": 10}' --accountId <accountId>.shardnet.near
  
  - Kiểm tra lý do bạn bị loại khỏi danh sách validator
  
        curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' 127.0.0.1:3030 | jq -c '.result.prev_epoch_kickout[] | select(.account_id | contains ("<POOL_ID>"))' | jq .reason
  
- Kiểm tra số block Produced / Expected 
  
        curl -r -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' 127.0.0.1:3030 | jq -c '.result.current_validators[] | select(.account_id | contains ("POOL_ID"))'
  
  
  Với 4 thử thách trên bạn đã bước đầu tạo được validator cho mình
  
  Nếu cần hỗ trợ hãy liên hệ tôi
  
  Discord
  
        Don20#6232
  
