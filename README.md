<h2 align=center>Nillion Verifier Node Guide</h2>

- Use this command to install docker on your system
```bash
sudo apt update -y && sudo apt install -y apt-transport-https ca-certificates curl software-properties-common && sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && sudo apt update -y && apt-cache policy docker-ce && sudo apt install -y docker-ce && sudo usermod -aG docker ${USER} && su - ${USER} -c "groups" && docker --version
```
- Use this command to pull nillion accuser image
```bash
docker pull nillion/retailtoken-accuser:v1.0.0
```
- Use the below command to create a directory and to initialise the accuser
```bash
mkdir -p nillion/accuser && docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 initialise
```
- After executing the above command, you will see `accound_id` and `public_key` in your terminal, copy the value
- Now visit [this site](https://verifier.nillion.com/verifier), submit your `accound_id` and `public_key` in the appropriate field
- Visit [faucet site](https://faucet.testnet.nillion.com/) to request faucet in your `account_id` you copied earlier
- Now run this command to get your accuser wallet private key
```bash
cat ~/nillion/accuser/credentials.json
```
- Copy the private key and save it, if you lose, you will not regain access to your accuser wallet
---
<h2 align=center>NOW TAKE A BREAK FOR 60 MINS</h2>

---
- After 60 mins, run these 2 final commands
```bash
sudo apt update && sudo apt install -y screen jq
```
```bash
current_block=$(curl -s https://testnet-nillion-rpc.lavenderfive.com/abci_info | jq -r '.result.response.last_block_height'); block_start=$((current_block - 5)); docker run -v $(pwd)/nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 accuse --rpc-endpoint "https://testnet-nillion-rpc.lavenderfive.com" --block-start $block_start
```
- Done ✅ , Join [AirdropNode](https://t.me/airdrop_node)
