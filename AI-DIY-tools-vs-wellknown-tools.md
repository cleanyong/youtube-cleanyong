| Project | What it does | Open-source CLI alternative(s) |
| --- | --- | --- |
| EdDSA-keygen | Generate/test Ed25519 keypair, export bin+Base64 | `ssh-keygen -t ed25519`, `openssl genpkey -algorithm ED25519` |
| adhoc-chat | Ephemeral 2-person chat (WebSocket server) | `ncat -l --chat` (Ncat), `weechat` (temp room) |
| alice-send | Alice DH keypair; derive secret with Bob pubkey | `openssl genpkey -genparam -algorithm DH` + `openssl pkeyutl -derive` |
| alice-sign | Sign JSON msg with local Ed25519 key, output pubkey | `openssl pkeyutl -sign -inkey key.pem -rawin` (Ed25519) |
| bob-send | Given Alice pubkey, produce Bob DH key + shared secret | Same as above `openssl genpkey`/`pkeyutl -derive` |
| bob-verify | Verify message/signature using stored Alice pubkey | `openssl pkeyutl -verify`, `openssl dgst -verify -signature sig.bin` |
| chat-encryption-helper | DH-handshake chat helper, AES-256 enc/dec | `signal-cli` (E2E chat) |
| cmd-call-kdbx | Search/create KeePass KDBX, generate keyfile | `keepassxc-cli show/find` |
| create-DNA-for-file | SHA-256 of file/STDIN → big int (dec/hex) | `sha256sum file`, `openssl dgst -sha256 file` |
| create-private-key | Generate DH private key/params (MODP14, etc.) | `openssl genpkey -algorithm DH -pkeyopt group:modp_2048` |
| decrypt-file | AES-256-CBC decrypt (password→SHA-256), output `.clear` | `openssl enc -aes-256-cbc -d -in file.enc -out file.clear -pass pass:...` |
| dilithium-keygen | ML-DSA-65/Dilithium3 keypair with test sign/verify | `openssl genpkey -provider oqsprovider -algorithm dilithium3` |
| dmg-util | Wrapper for macOS `hdiutil` to make encrypted APFS DMG | `hdiutil create -encryption AES-256 ...` |
| encrypt-file | AES-256-CBC encrypt (password→SHA-256), output `.enc` | `openssl enc -aes-256-cbc -salt -in file -out file.enc -pass pass:...` |
| find-big-prime | Generate large primes/safe primes (Miller–Rabin) | `openssl prime -generate -bits 2048` (add `-safe` for safe prime) |
| find-big-safe-prime | Concurrent safe prime generator p=2q+1 | `openssl prime -generate -bits 2048 -safe` |
| find-finger-print-for-file | Compute file SHA-256 fingerprint | `sha256sum file` |
| full-DH-with-sign | DH handshake with signatures + encrypted messages (web) | `openssl s_server/s_client` with ECDHE+certs, or `noise-cli`, `signal-cli` |
| gen-priv-dh | Generate DH private key, find generator g for p/q | `openssl genpkey -genparam -algorithm DH` (outputs p/g/q) |
| generate-password-for-cmd-line | Base62 password generator (36–45 chars) | `pwgen -s 44`, `apg -m36 -x45 -M SNCL` |
| jiming-pub-key-publish | Web form to store/share Base64 pubkeys (SQLite) | `gpg --send-keys <keyid>` (HKP), or `age-keygen` + `curl` to keyserver |
| kdbx-forum | Web forum using a single KeePass KDBX as DB | General forums: `discourse`/`nodebb` (CLI to run service) |
| kdf-argon2id | Argon2id password→key derivation CLI | `argon2 <pwd> -id -m 16 -t 3 -p 1 -l 32` |
| mac-monitoring | Monitor outbound TCP/UDP on macOS, log to file | `nettop -P -L 1 -n`, `lsof -i -P -n` |
| songmi-send-key-4-bob-use | TTL-based one-time secret/key sharing (AES-GCM) | `magic-wormhole send`, `onetimesecret` CLI/self-host |
| ssh-key-gen-ed25519 | Minimal ssh-keygen for Ed25519 | `ssh-keygen -t ed25519 -f id_ed25519 -C comment` |
