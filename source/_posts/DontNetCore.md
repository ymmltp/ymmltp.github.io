---
title: DontNetCore
date: 2022-01-05 10:09:11
tags: 学无止境
---

### Web Deploy发布
#### 1、不信任的证书
> Severity	Code	Description	Project	File	Line	Suppression State
Error		Web deployment task failed. (Connected to the remote computer ("10.136.16.135") using the specified process ("Web Management Service"), but could not verify the server’s certificate. If you trust the server, connect again and allow untrusted certificates.  

```html
在Properties->PublishProfiles->IISProfile.pubxml
文件中添加
<AllowUntrustedCertificate>True</AllowUntrustedCertificate>
```

