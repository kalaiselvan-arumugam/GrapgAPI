# Pick ONE: SECRET, PEM, PFX, JKS
azure.auth.mode=JKS

# Always present regardless of mode
azure.client.secret=YOUR_CLIENT_SECRET

azure.cert.path=/path/to/your/keystore
azure.cert.store.password=changeit
azure.cert.jks.alias=graph-api
azure.cert.jks.key.password=changeit
azure.cert.pfx.password=
```

### `AppProperties` — new `AuthMode` enum replaces `CertType`
```
AuthMode.SECRET  →  uses azure.client.secret
AuthMode.PEM     →  uses azure.cert.path
AuthMode.PFX     →  uses azure.cert.path + azure.cert.pfx.password
AuthMode.JKS     →  uses azure.cert.path + store/alias/key passwords
```

### `GraphClientConfig` — clean dispatch via `switch` on `AuthMode`
```
SECRET  →  ClientSecretCredential
PEM     →  ClientCertificateCredential (pemCertificate)
PFX     →  ClientCertificateCredential (pfxCertificate)
JKS     →  JKS → in-memory PKCS#12 → ClientCertificateCredential
