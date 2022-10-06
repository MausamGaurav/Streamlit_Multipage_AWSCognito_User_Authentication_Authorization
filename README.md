# Streamlit_Multipage_AWSCognito_User_Authentication_Authorization

1) The authenticate.py file is in the 'components' directory.
2) Before importing the authenticate.py file, we need to create a .env file in the 'components' directory with the correct values of the following variables. So, contents of the .env file might look like:

```
COGNITO_DOMAIN = "https://myappauthentication.auth.us-east-1.amazoncognito.com"
CLIENT_ID = "xyz"
CLIENT_SECRET = "secret-secret"
APP_URI = "http://localhost:8501/"
```
3) To authenticate, we need to import the authenticate module on every page, including the home page. The authentication can be performed/verified as below:

```
import components.authenticate as authenticate

# Check authentication when user lands on the page.
authenticate.set_st_state_vars()

# Add login/logout buttons
if st.session_state["authenticated"]:
    authenticate.button_logout()
else:
    authenticate.button_login()
```
4) We can hide/show page content using the state variables. For example:
```
if st.session_state["authenticated"] and "Underwriters" in st.session_state["user_cognito_groups"]:
    st.write(
        """This demo illustrates a combination of plotting and animation with
    Streamlit. We're generating a bunch of random numbers in a loop for around
    5 seconds. Enjoy!"""
    )

    # ...
else:
    if st.session_state["authenticated"]:
        st.write("You donot have access. Please contact the administrator.")
    else:
        st.write("Please login!")
```
