# How-to-deploy-webdollar-explorer-api
Deploy a WebDollar Blockchain Explorer API

### 1. Install Ubuntu 16.04
### 2. sudo apt update && sudo apt upgrade
### 3. Install the following:
```shell
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install -y build-essential linuxbrew-wrapper erlang libssl-dev:i386
curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh -o install_nvm.sh
bash install_nvm.sh
source ~/.profile
nvm install 8.2.1
nvm use 8.2.1
```
### 4. Install CouchDB:
```shell
curl -L https://couchdb.apache.org/repo/bintray-pubkey.asc | sudo apt-key add -
echo "deb https://apache.bintray.com/couchdb-deb xenial main" | sudo tee -a /etc/apt/sources.list
sudo apt update
sudo apt install couchdb -y
# config screen: standalone; bind IP: 127.0.0.1; password: password
```
### 5. Configure WebDollar Miner to use CouchDB
```shell
git clone https://github.com/WebDollar/Node-WebDollar.git
cd Node-WebDollar
COUCHDB_URL="http:\/\/admin:password@127.0.0.1:5984\/blockchaindb"
sed -i -e "s/blockchainDB3/${COUCHDB_URL}/g" "src/consts/const_global.js"
npm install
```
### 6. Start WebDollar Miner
```shell
screen # press space
npm run commands
# press 8 -> check if Blockchain is loading
# press ctrl + a and then d, to detach from screen
# screen -ls -> view screen_host
# screen -r screen_host <- connect to the screen
```
### 7. Clone WebDollar-Explorer-API
```shell
git clone https://github.com/thelazyprogrammer/webdollar-explorer-api.git
```
### 8. Start REST API
```shell
cd webdollar-explorer-api/server
npm install
npm run start
```
### 9. REST API ENDPOINTS
```http
# shows last 14 blocks
GET: /block

# shows block information
GET: /block/<block-id>

# shows miner information
GET: /miner/<miner_address>
```
### 10. Start Explorer Dashboard
```shell
cd client
npm install
npm run dev
```
