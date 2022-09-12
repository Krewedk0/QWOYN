```sh
cohod query game params
cohod query game whitelisted-contracts
cohod query game all-deposit-balances
cohod query game deposit-balance $(cohod keys show -a validator --keyring-backend=test)
cohod query game all-unbondings
cohod query game user-unbondings $(cohod keys show -a validator --keyring-backend=test)

# query liquidity & swap rate
cohod query game liquidity
cohod query game estimated-swap-out 10000ucoho
cohod query game estimated-swap-out 10000uqwoyn
cohod query game swap-rate

# deposit tokens
cohod tx game deposit-token 1000000stake --from=validator --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/ -y --broadcast-mode=block

# withdraw tokens
cohod tx game withdraw-token 500000stake --from=validator --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/ -y --broadcast-mode=block

# stake ingame token
cohod tx game stake-ingame-token 500000stake --from=validator --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/ -y --broadcast-mode=block

# begin unstake of ingame token
cohod tx game begin-unstake-ingame-token 100000stake --from=validator --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/ -y --broadcast-mode=block

# claim staking reward
cohod tx game claim-ingame-staking-reward --from=validator --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/ -y --broadcast-mode=block

# whitelist contract
cohod tx game whitelist-contracts coho14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9snm4thc --from=signer --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/ -y --broadcast-mode=block

# deposit nft from end wallet to game
cohod tx game deposit-nft coho14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9snm4thc 1 --from=signer --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/ -y --broadcast-mode=block

# query owner of nft
cohod query wasm contract-state smart coho14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9snm4thc '{"owner_of":{"token_id":"1"}}'

# game module address
# coho1djju4dm7wqk8s76vzjea80exht2rmfsxjx47wk

# instantiate ship nft with module account owned
cohod tx wasm instantiate 1 '{"name":"Ship NFT","symbol":"SHIP","minter":"coho1djju4dm7wqk8s76vzjea80exht2rmfsxjx47wk","owner":"coho1djju4dm7wqk8s76vzjea80exht2rmfsxjx47wk"}' --from validator --label "Ship-NFT" --chain-id test --gas auto --gas-adjustment 1.3 -b block --keyring-backend=test --home=$HOME/.cohod/ --no-admin -y

# transfer nft update ownership to module account - when owner is set to different account
cohod tx wasm execute coho14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9snm4thc '{"transfer_ownership":{"owner":"coho1djju4dm7wqk8s76vzjea80exht2rmfsxjx47wk"}}' --from signer --chain-id test --gas auto --gas-adjustment 1.3 -b block --keyring-backend=test --home=$HOME/.cohod/ -y


cohod tx game sign-withdraw-updated-nft coho14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9snm4thc 1 '{"update_nft":{"token_id":"1","extension":{"ship_type":67,"owner":"200"}}}' --from=signer --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/

cohod tx game withdraw-updated-nft coho14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9snm4thc 1 '{"update_nft":{"token_id":"1","extension":{"ship_type":67,"owner":"200"}}}' 42d6e9d3b62ffc9b0bc3f6a97cbc0857af1c7a7aa57549571d7bc72415a955d978a1790440ce53c8f9fbfa2ce70d967812eda6094d6f112d7e5736170e48e2a8 --from=signer --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/ -y --broadcast-mode=block --gas=400000

cohod tx game withdraw-updated-nft coho14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9snm4thc 2 '{"mint":{"token_id":"2","owner":"coho1djju4dm7wqk8s76vzjea80exht2rmfsxjx47wk","extension":{"ship_type":12,"owner":"300"}}}' --from=signer --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/ -y --broadcast-mode=block

# send tokens to admin to add liquidity
cohod tx bank send validator $(cohod keys show -a signer --keyring-backend=test) 1000000ucoho,1000000uqwoyn --from=validator --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/ -y --broadcast-mode=block
# add liquidity
cohod tx game add-liquidity 1000000ucoho,1000000uqwoyn --from=signer --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/ -y --broadcast-mode=block

cohod tx game swap 10000ucoho --from=validator --chain-id=qwoyn-1 --keyring-backend=test --home=$HOME/.cohod/ -y --broadcast-mode=block
```