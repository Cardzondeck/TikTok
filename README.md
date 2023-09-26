

# Check out this news
url = "https://www.pokeguardian.com/sets/upcoming-sets"

# Initialize the WebDriver (replace 'chrome' with your preferred browser)
driver = webdriver.Chrome()
driver.get(url)

# Replace 'your_element_locator' with the appropriate method to locate your element
element_locator = (By.ID, "your_element_id")

# Set up a loop to continuously check the element status
while True:
    try:
        # Wait for the element to be present on the page (adjust timeout as needed)
        WebDriverWait(driver, 10).until(EC.presence_of_element_located(element_locator))
        
        # Check the status of the element (replace with your own logic)
        element = driver.find_element(*element_locator)
        element_status = element.is_displayed()  # Example: Checking if the element is displayed

        # Print or log the status
        print(f"Element status: {element_status}")
        
        # Add logic to track the changes on GitHub (not covered here)

    except Exception as e:
        print(f"An error occurred: {str(e)}")