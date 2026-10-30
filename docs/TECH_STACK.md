# Technology stack

| Layer | Technology | Why it is used |
| --- | --- | --- |
| Mac application | Swift, AppKit and SwiftUI | Native independent windows, menus, panels and accessible controls |
| Text editing | AppKit text views and TextKit | Shared document buffers, incremental presentation and reusable editor views |
| Durable recovery | System SQLite, SHA-256 and LZFSE | Transactional metadata and revisions, content verification, compressed chunk sharing |
| Matching | Foundation/ICU regular expressions | Consistent literal/regex behavior across search scopes |
| Project discovery | Bundled ripgrep 15.2.0 | Ignore-aware file traversal with bounded helper output |
| Markdown preview | WebKit and bundled markdown-it 15.0.3 | Local rendering with explicit resource/navigation restrictions |
| Optional sync | Apple CloudKit | Private-account record synchronization and offline continuity |
| Trial and receipts | macOS Keychain and CryptoKit | Local trial state, device proof and signed license verification |
| Updates | Sparkle 2.10.0 | Signed feeds and archives, verified installation and relaunch |
| Commercial service | Cloudflare Workers, SQLite-backed Durable Objects and WebCrypto | Product-isolated license records, recovery and serialized activation limits |
| Payments | Stripe Managed Payments | Hosted checkout and verified provider events |
| Qualification | XCTest, process-isolated probes, native UI checks and Node tests | Editing regressions, recovery faults, memory workloads and commercial flows |

Dependency versions describe the privately qualified 1.0.0 (27) candidate. The public repository is documentation, not a buildable checkout. It does not contain app code, private backend code or credentials.

Markdown preview disables raw HTML and unsolicited network resources. Custom commands are different: they are programs the user explicitly chooses to run, with the user’s account permissions. See [privacy and boundaries](PRIVACY_AND_LOCAL_FIRST.md).

Third-party notices ship with the application. Each dependency retains its own license; TextRay’s documentation and artwork notice does not replace those licenses.
