# Only added a way to parse basegameid via command-line launch arguments
example cmd command: "start steam-ticket-generator.exe basegameid"
# Steam Ticket Generator 

This project provides an implementation of a encrypted app ticket generator for Steam. The generated ticket can then be used to run games that require a valid ticket to check for game ownership (ex. Denuvo protected games).

**Note for Denuvo games:**
 - Denuvo protected games will also require to have the correct steam account id in the steam emulator settings.
 - Each Steam account can achieve at most 5 activations a day.
 - An EncryptedAppTicket expires after 30 minutes and can be used multiple times in that time span, using the same ticket won't bypass the 5 daily activations limit.

## Usage

1. **Build the project:**

    ```sh
    cargo build --release
    ```

    The resulting binary will be located in `target/release/steam_ticket_generator.exe`.

2. **Provide the steam_api64.dll file:**

    Place the `steam_api64.dll` file in the same directory as the generated binary. This file is required to comunicate with the local Steam client.

3. **Run the generator:**

    Open steam on your computer, log in with the account you wish to use for the generation then run the program.
    Input the game's AppID when prompted. The program will use the currently logged in account to generate the ticket.
    It will output both the user's SteamID and the generated ticket in base64 format.

4. **Use the generated ticket:**
    It is possible to use the generated ticket with [gbe_fork](https://github.com/Detanup01/gbe_fork).
    Copy the generated SteamID and ticket to `configs.user.ini` in the `account_steamid` and `ticket` fields respectively.
    ```ini
    [user::general]
    account_steamid=YOUR_STEAM_ID
    ticket=BASE64_ENCODED_TICKET
    ```

## Builds

Builds are available in the [releases](https://github.com/denuvosanctuary/steam-ticket-generator/releases) section of the repository. Nightly builds are also available in the [actions](https://github.com/denuvosanctuary/steam-ticket-generator/actions) section.

The builds in the releases section will also include the `steam_api64.dll` file required to run the program. Otherwise you can download it from the [Steamworks SDK](https://partner.steamgames.com/doc/sdk). The minimum required version is 1.62.

## Linux

Linux builds are also now available in both [releases](https://github.com/denuvosanctuary/steam-ticket-generator/releases) and [actions](https://github.com/denuvosanctuary/steam-ticket-generator/actions). The required `libsteam_api.so` is already included in the releases.

## Disclaimer

This project is for educational and research purposes only. Use responsibly and respect software licenses.
