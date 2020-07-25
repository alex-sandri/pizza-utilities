# Pizza Utilities

## Usage

### Register the Service Worker
Add the following code at the top of every `<route-name>.route.ts` file.

```typescript
import * as pizza from "@alex-sandri/pizza-utilities";

pizza.ServiceWorker.register();
```

### Show install button

```typescript
let deferredPrompt?: any;

const installPwaButton = <HTMLButtonElement>document.querySelector("#install-pwa");

pizza.ServiceWorker.listen("beforeinstallprompt", e =>
{
    deferredPrompt = e;

    installPwaButton.style.display = "block";
});

installPwaButton.addEventListener("click", () =>
{
	deferredPrompt?.prompt();

	deferredPrompt?.userChoice.then((choiceResult: any) =>
	{
        if (choiceResult.outcome === "accepted")
            installPwaButton.style.display = "none";

		deferredPrompt = null;
	});
});
```

### Listen for app updates

```typescript
pizza.ServiceWorker.listen("updateready", () =>
{
    // TODO: Show a message to the user

    // After the user accepts the update
    pizza.ServiceWorker.update();
});
```
