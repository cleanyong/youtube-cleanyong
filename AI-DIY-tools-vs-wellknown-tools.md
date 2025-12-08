## 经过一个多月的DIY，我们已经建立围绕安全点线面的所有工具，这里把他们跟市面上的开源的命令行进行一个对比

# 中文
| 项目 | 功能 | 常见开源命令行替代 |
| --- | --- | --- |
| EdDSA-keygen | 生成/测试 Ed25519 密钥对并导出二进制+Base64 | `ssh-keygen -t ed25519`，`openssl genpkey -algorithm ED25519` |
| adhoc-chat | 临时 2 人聊天室（WebSocket 服务）-- 中文名：尬聊 | ... |
| alice-send | 生成 Alice 的 DH 私钥/公钥，可用 Bob 公钥算共享密钥 | `openssl genpkey -genparam -algorithm DH` + `openssl pkeyutl -derive` |
| alice-sign | 用本地 Ed25519 私钥签 JSON，输出公钥 | `openssl pkeyutl -sign -inkey key.pem -rawin`（Ed25519） |
| bob-send | 读取 Alice 公钥，生成 Bob DH 密钥并算共享密钥 | 同上 `openssl genpkey`/`pkeyutl -derive` |
| bob-verify | 用保存的 Alice 公钥验证消息签名 | `openssl pkeyutl -verify`，`openssl dgst -verify -signature sig.bin` |
| chat-encryption-helper | 基于 DH 握手的聊天 AES-256 加解密助手, 可以使用任何信道来传输，比如email，聊天室，论坛，短信etc | `signal-cli`（端到端加密聊天） |
| cmd-call-kdbx | KeePass KDBX 搜索/创建/生成 keyfile 的 CLI | `keepassxc-cli show/find` |
| create-DNA-for-file | 文件/STDIN 做 SHA-256，输出十进制/十六进制大整数 | `sha256sum file`，`openssl dgst -sha256 file` |
| create-private-key | 生成 DH 私钥/参数（MODP14 等） | `openssl genpkey -algorithm DH -pkeyopt group:modp_2048` |
| decrypt-file | AES-256-CBC 解密（密码取 SHA-256），输出 `.clear` | `openssl enc -aes-256-cbc -d -in file.enc -out file.clear -pass pass:...` |
| dilithium-keygen | 生成/测试 ML-DSA-65/Dilithium3 密钥对 | `openssl genpkey -provider oqsprovider -algorithm dilithium3` |
| dmg-util | 包装 `hdiutil` 创建加密 APFS DMG | 直接用 `hdiutil create -encryption AES-256 ...` |
| encrypt-file | AES-256-CBC 加密（密码取 SHA-256），输出 `.enc` | `openssl enc -aes-256-cbc -salt -in file -out file.enc -pass pass:...` |
| find-big-prime | 生成大素数/安全素数（Miller–Rabin） | `openssl prime -generate -bits 2048`（加 `-safe` 生成安全素数） |
| find-big-safe-prime | 并发生成安全素数 p=2q+1 | `openssl prime -generate -bits 2048 -safe` |
| find-finger-print-for-file | 计算文件 SHA-256 指纹 | `sha256sum file` |
| full-DH-with-sign | 带签名的 DH 握手 + 加密消息（Web 服务） | `openssl s_server/s_client`（ECDHE+证书），或 `noise-cli`、`signal-cli` |
| gen-priv-dh | 生成 DH 私钥，给定 p/q 寻找生成元 g | `openssl genpkey -genparam -algorithm DH`（输出 p/g/q） |
| generate-password-for-cmd-line | 生成 36–45 位 Base62 密码 | `pwgen -s 44`，`apg -m36 -x45 -M SNCL` |
| jiming-pub-key-publish | Web 表单存储/分享 Base64 公钥（SQLite） | `gpg --send-keys <keyid>`（HKP），或 `age-keygen` + `curl` 到 keyserver |
| kdbx-forum | 用单个 KeePass KDBX 作为“论坛数据库”的 Web 服务，跟朋友们呼唤 .kdbx 文件就行 | NA |
| kdf-argon2id | Argon2id 密码派生 CLI | `argon2 <pwd> -id -m 16 -t 3 -p 1 -l 32` |
| mac-monitoring | 监控 macOS 出站 TCP/UDP，记录日志 | `nettop -P -L 1 -n`，`lsof -i -P -n` |
| songmi-send-key-4-bob-use | 带 TTL 的一次性密钥/秘密分享（AES-GCM） | `magic-wormhole send`，`onetimesecret` CLI/自建 |
| ssh-key-gen-ed25519 | 极简版 ssh-keygen 生成 Ed25519 | `ssh-keygen -t ed25519 -f id_ed25519 -C comment` |



## English

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
