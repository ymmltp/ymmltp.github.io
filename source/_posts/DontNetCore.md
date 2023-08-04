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


### Web Api
> ApiController: 当在控制器类上应用了 ApiController 特性时，它会启用复杂类型参数绑定功能。可以传递List<myclass> 作为 request body，但是会导致int 这种简单参数无法获取到 。
> 
> 不推荐使用 ApiController，想获取复杂类型的参数，可以直接使用 FromBody 定义函数的参数来源

```c
 public IActionResult AddLists( [FromBody] List<ReminderContact> items) 
```
> Route("[controller]/[action]") : 用于定义 API 控制器的行为和路由。
```C
namespace Esclate_Reminder.Controllers
{
    [ApiController]
    [Route("[controller]/[action]")]
    public class EscalateContactController : Controller
    {
        private EsclateContactService _escService = new EsclateContactService();
        [HttpGet]
        public IActionResult QueryEnable()
        {
            try
            {
                return Json(_escService.QueryEnable());
            }
            catch (Exception err)
            {
                return new CustomError(HttpStatusCode.BadRequest, err.Message);
            }
        }
        [HttpGet]
        public IActionResult QueryAll()
        {
            try
            {
                return Json(_escService.QueryAll());
            }
            catch (Exception err)
            {
                return new CustomError(HttpStatusCode.BadRequest, err.Message);
            }
        }
        [HttpGet]
        public IActionResult Query_byCategory(string category)
        {
            try
            {
                return Json(_escService.Query_byCategory(category));
            }
            catch (Exception err)
            {
                return new CustomError(HttpStatusCode.BadRequest, err.Message);
            }
        }

        [HttpPost]
        public IActionResult AddLists(List<ReminderContact> items) {
            try
            {
                return Json(_escService.AddLists(items));
            }
            catch (Exception err)
            {
                return new CustomError(HttpStatusCode.BadRequest, err.Message);
            }
        }

        [HttpPost]
        public IActionResult Add(ReminderContact item)
        {
            try
            {
                return Json(_escService.Add(item));
            }
            catch (Exception err)
            {
                return new CustomError(HttpStatusCode.BadRequest, err.Message);
            }
        }
    }
}
```