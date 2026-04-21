# CapMonster Cloud Go client

Official Go SDK for the CapMonster Cloud API.

## Links

- Documentation: [docs.capmonster.cloud](https://docs.capmonster.cloud/)
- Dashboard / API key: [dash.capmonster.cloud](https://dash.capmonster.cloud/)
- Module path: `github.com/ZennoLab/capmonstercloud-client-go`

💵 Want to test before depositing? Contact support and we’ll add trial credits to your account.

## Installation

```bash
go get github.com/ZennoLab/capmonstercloud-client-go
```

The import path remains `github.com/ZennoLab/capmonstercloud-client-go` for compatibility.

## Minimal example
```go
package main

import (
	"fmt"

	"github.com/ZennoLab/capmonstercloud-client-go/pkg/client"
	"github.com/ZennoLab/capmonstercloud-client-go/pkg/tasks"
)

func main() {
	client := client.New("YourClientKey")

	//get balance
	if balance, err := client.GetBalance(); err != nil {
		fmt.Println(err)
	} else {
		fmt.Println(balance)
	}

	// solve RecaptchaV2 (without proxy)
	recaptchaV2Task := tasks.NewRecaptchaV2TaskProxyless(
		"https://lessons.zennolab.com/captchas/recaptcha/v2_simple.php?level=high",
		"6Lcg7CMUAAAAANphynKgn9YAgA4tQ2KI_iqRyTwd",
	)
	noCache := false
	if result, err := client.SolveRecaptchaV2Proxyless(recaptchaV2Task, noCache, nil); err != nil {
		fmt.Println(err)
	} else {
		fmt.Println(result)
	}

	// solve ImageToTextTask with module
	imgToTextTask := tasks.NewImageToTextTask("BODY").WithCapMonsterModule(tasks.CapMonsterModuleGoogle)
	if result, err := client.SolveImageToText(imgToTextTask, nil); err != nil {
		fmt.Println(err)
	} else {
		fmt.Println(result)
	}
}
```

Supported task families include reCAPTCHA, GeeTest, Turnstile, image-to-text, and additional task types documented in the public docs.

Supported request classes:

- [GeeTestProxylessRequest](https://zenno.link/doc-geetest-en)
- [GeeTestRequest](https://zenno.link/doc-geetest-proxy-en)
- [HCaptchaProxylessRequest](https://zenno.link/doc-hcaptcha-en)
- [HCaptchaRequest](https://zenno.link/doc-hcaptcha-proxy-en)
- [ImageToTextRequest](https://zenno.link/doc-ImageToTextTask-en)
- [RecaptchaV2ProxylessRequest](https://zenno.link/doc-recaptcha2-en)
- [RecaptchaV2Request](https://zenno.link/doc-recaptcha2-proxy-en)
- [RecaptchaV3ProxylessRequest](https://zenno.link/doc-recaptcha3-en)
- [RecaptchaV2EnterpriseProxylessRequest](https://zenno.link/doc-recaptcha2e-en)
- [RecaptchaV2EnterpriseRequest](https://zenno.link/doc-recaptcha2e-proxy-en)
- [TurnstileProxylessRequest](https://zenno.link/doc-turnstile-en)
- [TurnstileRequest](https://zenno.link/doc-turnstile-proxy-en)
- [RecaptchaComplexImageTaskRequest](https://zenno.link/doc-complextask-rc-en)
- [HcaptchaComplexImageTaskRequest](https://zenno.link/doc-complextask-hc-en)
