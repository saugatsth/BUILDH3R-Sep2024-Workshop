# BUILDH3R Sept Leo

## System Setup
-  Install `rust` locally. Below command will install cli. [More deatils](https://www.rust-lang.org/tools/install)
    ```sh
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    ```

- Install `leo`. [More Details](https://github.com/ProvableHQ/leo/):
    ```sh
    # Download the source code
    git clone https://github.com/ProvableHQ/leo/
    cd leo
    git checkout testnet-beta
    cargo install --path .
    ```

- Install `SnarkOS`. [More Details](https://github.com/ProvableHQ/snarkOS):
    ```sh
    git clone https://github.com/AleoHQ/snarkOS.git --depth 1
    cd snarkOS
    git checkout testnet-beta
    ./build_ubuntu.sh
    cargo install --path .
    ```

- Install SnarkVM. [More Details](https://github.com/ProvableHQ/snarkVM):
    ```sh
    cargo install snarkvm
    ```

- Make sure all the binaries are added in PATH.

## Create Aleo Project
### Create new project:
- Command:
    ```sh
    leo new tsmbughunter_leo_auction
    ```

- Since, we are trying to create an auction app, there must be bidder and owner. So let's create 2 bidder account and 1 owner.
- Command:
    ```sh
    snarkos account new
    ```
- So, run above command 3 times in terminal:
    <details><summary> Detailed Output </summary><blockquote>

    ~~~
    $ snarkos account new

    Private Key  <redacted>
        View Key  <redacted>
        Address  aleo1rdszsdqcm3y0fztxzhpzqydqs07qgmtatl9slypyl0hw8lxpnyxqlrt2ct

    $ snarkos account new

    Private Key  <redacted>
        View Key  <redacted>
        Address  aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k

    $ snarkos account new

    Private Key  <redacted>
        View Key  <redacted>
        Address  aleo1ntg2wewwf0l3yuulkjnua4lsukf0zujxrrqkharkxq4eat0axsqq42r3gn
    ~~~
    
    </blockquote></details>

- In above image, suppose 1 a/c with Address `aleo1rdszsdqcm3y0fztxzhpzqydqs07qgmtatl9slypyl0hw8lxpnyxqlrt2ct` is owner and remaining 2nd and 3rd a/cs are bidders. 

- Modify `auction/src/main.leo`. Do not forget to replace owner address in `main.leo` file.

- `.env` is created during the creation of the project. By default, it contains:
    ```sh
    NETWORK=testnet
    PRIVATE_KEY=APrivateKey1zkp8CZNn3yeCseEtxuVPbDCwSyhGW6yZKUYKfgXmcpoGPWH
    ENDPOINT=https://api.explorer.aleo.org/v1
    ```

- Value of Endpoint must be changed with: `https://api.explorer.provable.com/v1`
- New `.env`:
    ```sh
    NETWORK=testnet
    PRIVATE_KEY=APrivateKey1zkp8CZNn3yeCseEtxuVPbDCwSyhGW6yZKUYKfgXmcpoGPWH
    ENDPOINT=https://api.explorer.provable.com/v1
    ```

### Run Test
#### 1st Bid:
- Now, the value of `PRIVATE_KEY` in `.env` must be replaced with the `PRIVATE_KEY` of the 1st bidder.
- Run `place_bid` transaction:
    - Code Snippet:
        ```sh
        leo run place_bid <Address> <Amount>
        ```
    
    - Command:
        ```sh
        leo run place_bid aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k 900u64
        ```
        <details><summary> Detailed Output </summary><blockquote>

        ~~~
        $ leo run place_bid aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k 900u64
            Leo ✅ Compiled 'tsmbughunter_leo_auction.aleo' into Aleo instructions

        ⛓  Constraints

        •  'tsmbughunter_leo_auction.aleo/place_bid' - 2,026 constraints (called 1 time)

        ➡️  Output

        • {
        owner: aleo1rdszsdqcm3y0fztxzhpzqydqs07qgmtatl9slypyl0hw8lxpnyxqlrt2ct.private,
        bidder: aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        amount: 900u64.private,
        is_winner: false.private,
        _nonce: 6830832920207394116428396672567686448167056875594237238497676755910882609135group.public
        }

            Leo ✅ Finished 'tsmbughunter_leo_auction.aleo/place_bid'
        ~~~

        </blockquote></details>
       
        <img src="./Assets/1st-bidder.png">
        
#### 2nd Bid:
- Now, the value of `PRIVATE_KEY` in `.env` must be replaced with the `PRIVATE_KEY` of the 2nd bidder.
- Run `place_bid` transaction:
    - Code Snippet:
        ```sh
        leo run place_bid <Address> <Amount>
        ```
    
    - Command:
        ```sh
        leo run place_bid aleo1ntg2wewwf0l3yuulkjnua4lsukf0zujxrrqkharkxq4eat0axsqq42r3gn 555u64
        ```
        <details><summary> Detailed Output </summary><blockquote>

        ~~~
        $ leo run place_bid aleo1ntg2wewwf0l3yuulkjnua4lsukf0zujxrrqkharkxq4eat0axsqq42r3gn 555u64
            Leo ✅ Compiled 'tsmbughunter_leo_auction.aleo' into Aleo instructions

        ⛓  Constraints

        •  'tsmbughunter_leo_auction.aleo/place_bid' - 2,026 constraints (called 1 time)

        ➡️  Output

        • {
        owner: aleo1rdszsdqcm3y0fztxzhpzqydqs07qgmtatl9slypyl0hw8lxpnyxqlrt2ct.private,
        bidder: aleo1ntg2wewwf0l3yuulkjnua4lsukf0zujxrrqkharkxq4eat0axsqq42r3gn.private,
        amount: 555u64.private,
        is_winner: false.private,
        _nonce: 1904999836641957260477443834719153790041655364141728438021761183397454707260group.public
        }

            Leo ✅ Finished 'tsmbughunter_leo_auction.aleo/place_bid'
        ~~~

        </blockquote></details>
       
        <img src="./Assets/2nd-bidder.png">

#### Resolve Time:
- Since, both the bidder has succesfully bidded, it is the time of owner to resolve who wins the bid.
- Now, the value of `PRIVATE_KEY` in `.env` must be replaced with the `PRIVATE_KEY` of the owner.
- Run `resolve` transaction:
    - Code Snippet:
        ```sh
        leo run resolve <Output_Of_1st_Bid> <Output_Of_2nd_Bid>
        ```
    
    - Command:
        ```sh
        leo run resolve '{
        owner: aleo1rdszsdqcm3y0fztxzhpzqydqs07qgmtatl9slypyl0hw8lxpnyxqlrt2ct.private,
        bidder: aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        amount: 900u64.private,
        is_winner: false.private,
        _nonce: 6830832920207394116428396672567686448167056875594237238497676755910882609135group.public
        }' '{
        owner: aleo1rdszsdqcm3y0fztxzhpzqydqs07qgmtatl9slypyl0hw8lxpnyxqlrt2ct.private,
        bidder: aleo1ntg2wewwf0l3yuulkjnua4lsukf0zujxrrqkharkxq4eat0axsqq42r3gn.private,
        amount: 555u64.private,
        is_winner: false.private,
        _nonce: 1904999836641957260477443834719153790041655364141728438021761183397454707260group.public
        }'
        ```
        <details><summary> Detailed Output </summary><blockquote>

        ~~~
        $ leo run resolve '{
        owner: aleo1rdszsdqcm3y0fztxzhp> zqydqs07qgmtatl9slypyl0hw8lxpnyxqlrt2ct.private,
        b> idder: aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        amount: 900u64.priva> te,
        is_winner: false.private,
        _nonce: 683083292020> > 7394116428396672567686448167056875594237238497676755910882609135group.public
        }' '{
        owner: aleo1rdszs> > dqcm3y0fztxzhpzqydqs07qgmtatl9slypyl0hw8lxpnyxqlrt2ct.private,
        bidder: aleo1ntg2wewwf0l3yuulkjnua4ls> ukf0zujxrrqkharkxq4eat0axsqq42r3gn.private,
        amount> : 555u64.private,
        is_winner: false.private,
        _nonce> > : 1904999836641957260477443834719153790041655364141728438021761183397454707260group.public
        }'> 
            Leo ✅ Compiled 'tsmbughunter_leo_auction.aleo' into Aleo instructions

        ⛓  Constraints

        •  'tsmbughunter_leo_auction.aleo/resolve' - 2,161 constraints (called 1 time)

        ➡️  Output

        • {
        owner: aleo1rdszsdqcm3y0fztxzhpzqydqs07qgmtatl9slypyl0hw8lxpnyxqlrt2ct.private,
        bidder: aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        amount: 900u64.private,
        is_winner: false.private,
        _nonce: 1825194326246347271594001688991752349558936976990968492486466867932633330371group.public
        }

            Leo ✅ Finished 'tsmbughunter_leo_auction.aleo/resolve' 
        ~~~

        </blockquote></details>
       
        <img src="./Assets/bid-resolve.png">

#### Finish Bid:
- Keep same `.env` as we are running as owner.
- Run `finish` transaction:
    - Code Snippet:
        ```sh
        leo run finish <Resolve_Bid>
        ```
    
    - Command:
        ```sh
        leo run finish '{
        owner: aleo1rdszsdqcm3y0fztxzhpzqydqs07qgmtatl9slypyl0hw8lxpnyxqlrt2ct.private,
        bidder: aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        amount: 900u64.private,
        is_winner: false.private,
        _nonce: 1825194326246347271594001688991752349558936976990968492486466867932633330371group.public
        }'
        ```
        <details><summary> Detailed Output </summary><blockquote>

        ~~~
        $ leo run finish '{
        owner: aleo1rdszsdqcm3y0fztxzhpz> qydqs07qgmtatl9slypyl0hw8lxpnyxqlrt2ct.private,
        bi> dder: aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        amount: 900u64.privat> e,
        is_winner: false.private,
        _nonce: 1825194326246> > 347271594001688991752349558936976990968492486466867932633330371group.public
        }'> 
            Leo ✅ Compiled 'tsmbughunter_leo_auction.aleo' into Aleo instructions

        ⛓  Constraints

        •  'tsmbughunter_leo_auction.aleo/finish' - 2,026 constraints (called 1 time)

        ➡️  Output

        • {
        owner: aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        bidder: aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        amount: 900u64.private,
        is_winner: true.private,
        _nonce: 7851700378226979219966084349771158805332620178699958837693064328074541323850group.public
        }

            Leo ✅ Finished 'tsmbughunter_leo_auction.aleo/finish'
        ~~~

        </blockquote></details>
       
        <img src="./Assets/finish-bid.png">

    - According to above outputs, a/c with `Address`: `aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k` is the winner and is new owner.

#### Claim Bid:
- Now, the value of `PRIVATE_KEY` in `.env` must be replaced with the `PRIVATE_KEY` of the owner `aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k`.
- Run `claim` transaction:
    - Code Snippet:
        ```sh
        leo run claim <Finish_Bid>
        ```
    
    - Command:
        ```sh
        leo run claim '{
        owner: aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        bidder: aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        amount: 900u64.private,
        is_winner: true.private,
        _nonce: 7851700378226979219966084349771158805332620178699958837693064328074541323850group.public
        }'
        ```
        <details><summary> Detailed Output </summary><blockquote>

        ~~~
        $ leo run claim '{
        owner: aleo12wgjumuumwjtf5djw7x38> j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        bid> der: aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        amount: 900u64.private> ,
        is_winner: true.private,
        _nonce: 785170037822697> > 9219966084349771158805332620178699958837693064328074541323850group.public
        }'> 
            Leo ✅ Compiled 'tsmbughunter_leo_auction.aleo' into Aleo instructions

        ⛓  Constraints

        •  'tsmbughunter_leo_auction.aleo/claim' - 2,021 constraints (called 1 time)

        ➡️  Output

        • {
        owner: aleo12wgjumuumwjtf5djw7x38j9qpy3e4cs357xl9efpty507jpcgvysy5g66k.private,
        amount: 900u64.private,
        _nonce: 453440471127476076647758735186060578421733188538490203334306737280271306973group.public
        }

            Leo ✅ Finished 'tsmbughunter_leo_auction.aleo/claim' 
        ~~~

        </blockquote></details>
       
        <img src="./Assets/claim-bid.png">

#### Deploy To Testnet:
- Command:
    ```sh
    leo deploy --network testnet
    ```


    <details><summary> Detailed Output </summary><blockquote>

    ~~~
    $ leo deploy --network testnet
        Leo ✅ Compiled 'tsmbughunter_leo_auction.aleo' into Aleo instructions
    📦 Creating deployment transaction for 'tsmbughunter_leo_auction.aleo'...


    Base deployment cost for 'tsmbughunter_leo_auction.aleo' is 11.4151 credits.

    +-------------------------------+----------------+
    | tsmbughunter_leo_auction.aleo | Cost (credits) |
    +-------------------------------+----------------+
    | Transaction Storage           | 2.786000       |
    +-------------------------------+----------------+
    | Program Synthesis             | 7.629100       |
    +-------------------------------+----------------+
    | Namespace                     | 1.000000       |
    +-------------------------------+----------------+
    | Priority Fee                  | 0.000000       |
    +-------------------------------+----------------+
    | Total                         | 11.415100      |
    +-------------------------------+----------------+

    Your current public balance is 12 credits.

    ? Do you want to submit deployment of program `tsmbughunter_leo_auction.aleo.aleo` to network testnet via endpoint https://api.explorer.provable.com/v1 using address aleo1rdszsdqcm3y0fztxzhpz
    ✔ Do you want to submit deployment of program `tsmbughunter_leo_auction.aleo.aleo` to network testnet via endpoint https://api.explorer.provable.com/v1 using address aleo1rdszsdqcm3y0fztxzhpzqydqs07qgmtatl9slypyl0hw8lxpnyxqlrt2ct? · yes
    ✅ Created deployment transaction for 'tsmbughunter_leo_auction.aleo'

    Broadcasting transaction to https://api.explorer.provable.com/v1/testnet/transaction/broadcast...

    ⌛ Deployment at14d064zuwxh7jf8rvlmxu07tqu5xercv2a3jwvc25746qwpjg8sxqggs8sy ('tsmbughunter_leo_auction.aleo') has been broadcast to https://api.explorer.provable.com/v1/testnet/transaction/broadcast.
    ~~~

    </blockquote></details>

    <img src="./Assets/deploy-to-testnet.png">


- Links: 
    - Aleo Program: [https://testnet.aleo.info/program/tsmbughunter_leo_auction.aleo](https://testnet.aleo.info/program/tsmbughunter_leo_auction.aleo)
    - Deploy Txn: [https://testnet.aleo.info/transaction/at14d064zuwxh7jf8rvlmxu07tqu5xercv2a3jwvc25746qwpjg8sxqggs8sy](https://testnet.aleo.info/transaction/at14d064zuwxh7jf8rvlmxu07tqu5xercv2a3jwvc25746qwpjg8sxqggs8sy) 

    <img src="./Assets/testnet-program.png">