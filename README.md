# AUTOMATION-TESTING
## ASSIGNMENT 

### ACTOR.PY: 
```
import time 

from selenium import webdriver 

 

driver = webdriver.Chrome() 

 

try: 

    # Open Google and search for Dhanush 

    driver.get("https://www.google.com/search?q=Dhanush") 

    time.sleep(10) 

    input("Press Enter to close the browser...") 

 

finally: 

    driver.quit() 

 ```

### OUTPUT:
<img width="1202" height="927" alt="Screenshot 2026-10-05 141306" src="https://github.com/user-attachments/assets/d2436927-7639-44d4-939b-b8b14978754b" />


PRODUCT.PY: 
```
import time

from selenium import webdriver
from selenium.webdriver.common.by import By

# Open Chrome
driver = webdriver.Chrome()

try:
    # Open SauceDemo
    driver.get("https://saucedemo.com")

    # Find login elements
    username = driver.find_element(By.ID, "user-name")
    password = driver.find_element(By.NAME, "password")
    login = driver.find_element(By.ID, "login-button")

    # Enter username and password
    username.send_keys("standard_user")
    password.send_keys("secret_sauce")

    # Click login
    login.click()

    # Wait for products page
    time.sleep(2)

    # Find all product names
    products = driver.find_elements(By.CLASS_NAME, "inventory_item_name")

    # Print product names
    print("\nAll Products:")
    print("-------------------------")

    for product in products:
        print(product.text)

    print("-------------------------")
    print("Total products:", len(products))

    # Keep browser open
    time.sleep(5)

finally:
    driver.quit()
```
### OUTPUT:
<img width="1275" height="976" alt="Screenshot 2026-10-05 141555" src="https://github.com/user-attachments/assets/35202944-5def-4a7e-b787-1bbfc09365f3" />

## FLIPKART.PY
```
import time

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from webdriver_manager.chrome import ChromeDriverManager


def flipkart_login():

    # =========================================================
    # 1. CHROME SETUP
    # =========================================================

    options = webdriver.ChromeOptions()
    options.add_argument("--start-maximized")

    print("[*] Starting Chrome Driver...")

    service = Service(ChromeDriverManager().install())

    driver = webdriver.Chrome(
        service=service,
        options=options
    )

    # Give each Selenium wait up to 30 seconds
    wait = WebDriverWait(driver, 30)

    # Allow the browser up to 60 seconds to load a page
    driver.set_page_load_timeout(60)

    try:

        # =====================================================
        # 2. OPEN FLIPKART LOGIN PAGE
        # =====================================================

        print("[*] Opening Flipkart Login Page...")

        driver.get("https://www.flipkart.com/account/login")

        print("[*] Page loaded.")

        # =====================================================
        # 3. ENTER MOBILE NUMBER
        # =====================================================

        phone_num = input(
            "Enter your 10-digit Flipkart registered mobile number: "
        ).strip()

        print("[*] Waiting for mobile number field...")

        phone_input = wait.until(
            EC.visibility_of_element_located(
                (
                    By.XPATH,
                    "//input[@type='text' or @type='tel']"
                )
            )
        )

        phone_input.clear()
        phone_input.send_keys(phone_num)

        print("[*] Mobile number entered.")

        # =====================================================
        # 4. REQUEST OTP
        # =====================================================

        print("[*] Waiting for Request OTP button...")

        request_otp_btn = wait.until(
            EC.element_to_be_clickable(
                (
                    By.XPATH,
                    "//button[contains(., 'Request OTP')]"
                )
            )
        )

        request_otp_btn.click()

        print("[*] OTP requested.")

        # =====================================================
        # 5. MANUAL OTP ENTRY
        # =====================================================

        print("\n" + "=" * 50)

        otp = input(
            ">>> Enter the OTP received on your phone: "
        ).strip()

        print("=" * 50 + "\n")

        # =====================================================
        # 6. FIND OTP INPUT
        # =====================================================

        print("[*] Waiting for OTP field...")

        otp_inputs = wait.until(
            EC.presence_of_all_elements_located(
                (
                    By.XPATH,
                    "//input[@type='text' or @type='tel']"
                )
            )
        )

        # =====================================================
        # 7. ENTER OTP
        # =====================================================

        if len(otp_inputs) == 1:

            otp_inputs[0].send_keys(otp)

        else:

            for index, digit in enumerate(otp):

                if index < len(otp_inputs):

                    otp_inputs[index].send_keys(digit)

        print("[*] OTP entered.")

        # =====================================================
        # 8. VERIFY / SUBMIT
        # =====================================================

        print("[*] Waiting for Verify button...")

        submit_btn = wait.until(
            EC.element_to_be_clickable(
                (
                    By.XPATH,
                    "//button[contains(., 'Verify') or contains(., 'Submit')]"
                )
            )
        )

        submit_btn.click()

        print("[*] OTP submitted.")

        # =====================================================
        # 9. WAIT FOR LOGIN TO COMPLETE
        # =====================================================

        print("[*] Waiting for login to complete...")

        time.sleep(50)

        print("[+] Login process completed.")

        # Keep browser open
        input(
            "\nPress ENTER in console to close the browser..."
        )

    except Exception as e:

        print("\n[!] Error encountered:")
        print(e)

        input(
            "\nPress ENTER to close the browser..."
        )

    finally:

        driver.quit()


# =============================================================
# PROGRAM START
# =============================================================

if __name__ == "__main__":
    flipkart_login()
```
### OUTPUT:
<img width="1887" height="1077" alt="Screenshot 2026-10-05 142559" src="https://github.com/user-attachments/assets/43ea6ab6-079b-41f2-b047-eddb0059a2a7" />
<img width="1768" height="952" alt="Screenshot 2026-10-05 142620" src="https://github.com/user-attachments/assets/ac753df7-6f82-4c88-92b8-b7be43264e26" />
<img width="1526" height="762" alt="Screenshot 2026-10-05 142729" src="https://github.com/user-attachments/assets/a8289757-b2f1-452b-b858-d07306e6a4f1" />


