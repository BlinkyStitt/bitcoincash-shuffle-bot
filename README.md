# Cash Shuffle Liquidity Bot in Docker

Based on [this guide](https://www.yours.org/content/how-to-run-your-own-cash-shuffle-liquidity-bot--in-9-sorta-simple-step-2d991b4e4d2c).

**IMPORTANT!** This is brand new and barely tested. Do not use large amounts with this yet!

1. Install [docker](https://www.docker.com/community-edition)

2. Create `~/docker/bitcoincash-shuffle/docker-compose.yml`:

    ```yaml
    version: '2.3'

    volumes:
      electron_cash_data:
      tor_var:

    services:
      bot:
        image: bwstitt/bitcoincash-shuffle-bot
        restart: always
        volumes:
          - electron_cash_data:/home/abc/.electron-cash      
          - tor_var:/var/lib/tor
    ```

3. Run all `docker-compose` commands from next to your docker-compose.yml:

    ```bash
    cd ~/docker/bitcoincash-shuffle
    ```

4. Start the bot:

    ```bash
    docker-compose up --pull -d
    ```

5. Show your seed so that you can back it up! Do not proceed without backing it up securely!

    ```bash
    docker-compose exec bot grep seed "/home/abc/.electron-cash/wallets/default_wallet"
    ```

6. List some unused addresses:

    ```bash
    docker-compose exec -u abc bot electron-cash listaddresses --unused
    ```

7. Send 0.02 BCH or more (but not much more, this is still early code!) to 3 different addresses in your wallet.

8. Watch the logs:

    ```bash
    docker-compose logs -f
    ```

## TODO
- Better docs
- Document Nyx
- Don't put passwords in command line args. Use files with proper user permissions instead.
- allow customizing all the flags with env vars
- connect to .onion server
- bot.py should read password from file instead of passing as an argument
- typo "sutisfiying"
- bot.py should allow choosing the electrum server, too. right now can only choose the shuffle server
- don't share the entire ~/.electron-cash with the host
- document using an existing wallet
