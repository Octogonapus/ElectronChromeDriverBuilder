# ElectronChromeDriverBuilder

This project builds [chromedriver](https://www.selenium.dev/documentation/webdriver/getting_started/install_drivers/) artifacts for use in Julia with [Electron.jl](https://github.com/davidanthoff/Electron.jl).

## Usage

Add these artifacts to your `Artifacts.toml` file following these docs: https://pkgdocs.julialang.org/v1/artifacts/

The tagging in this repo is the same as in [ElectronBuilder](https://github.com/davidanthoff/ElectronBuilder) so that you can match the tags.
It is important to use the proper version of `chromedriver` with Electron.jl.

### Example Code

In Julia, open an Electron app:

```julia
using Electron
app = Application(additional_electron_args = ["--remote-debugging-port=7070", "--user-data-dir=/path/to/some/directory"])
win = Window(app, URI("file://main.html"))
```

Then in Python, you can run Selenium:

```python
# Note: you must have the /path/to/chromedriver on your PATH!

from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.options import Options
from selenium import webdriver

chrome_options = Options()
chrome_options.add_experimental_option("debuggerAddress", "127.0.0.1:7070")
driver = webdriver.Chrome(options=chrome_options)

btn = driver.find_element(By.ID, "some-button")
print(btn)
btn.click()

# don't close the driver because Julia manages the Electron process
# driver.close()
```
