# Edge-Extensions

Reside Residential's Microsoft Edge extensions, hosted here with GitHub Pages so Intune can install and update them on company computers.

| Extension | File | Version | Extension ID |
|---|---|---|---|
| Therap Receipt Uploader | `therap-receipt-uploader.crx` | 1.8.4 | `jaagbiajmmmnhpepnocdhljdpjikflih` |
| Therap Ledger Checker | `therap-ledger-checker.crx` | 1.3.8 | `djjaimnggaapmooealilnikiidakidpg` |
| TrueLink Receipt Checker | `truelink-receipt-checker.crx` | 1.8.1 | `bdijikkgckcfmenegipgemmfnjgokbco` |

## Files

- **`*.crx`**: the packed extensions, ready to install.
- **`update.xml`**: the update manifest Edge checks. It lists each extension's ID, version and download address.
- **`.gitignore`**: keeps the private `.pem` keys out of this public repository.

## Intune

In Intune, under **Microsoft Edge > Extensions > Control which extensions are installed silently** (ExtensionInstallForcelist), add one line per extension:

```
jaagbiajmmmnhpepnocdhljdpjikflih;https://resideresidential.github.io/Edge-Extensions/update.xml
djjaimnggaapmooealilnikiidakidpg;https://resideresidential.github.io/Edge-Extensions/update.xml
```

All three use the same `update.xml`.

The TrueLink Receipt Checker is for the finance office only, so it is not in the list above. To install it on one computer through Intune, add this line in a policy assigned to just that computer or user:

```
bdijikkgckcfmenegipgemmfnjgokbco;https://resideresidential.github.io/Edge-Extensions/update.xml
```

## Releasing an update

1. Raise `"version"` in the extension's `manifest.json`.
2. Pack it in Edge (`edge://extensions` > Developer mode > **Pack extension**) and choose the extension's existing `.pem` key. A different key gives a different ID, and Edge treats it as a different extension.
3. Replace the `.crx` here, change its `version` in `update.xml`, and commit.

Edge checks for updates every few hours. Never commit a `.pem` file.
