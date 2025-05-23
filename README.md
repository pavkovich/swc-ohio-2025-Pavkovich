# # # # #
# NITIC - Secure Programming with Python Assessment
# swc-ohio-2025-Pavkovich
#
# Developer Name: Robert Pavkovich
# Email: rpavkovich@cscc.edu
# College Name: Columbus State Community College
# Creation Date: May 23, 2025 @ 9:00 AM
# # # # #
#
# Professor: Pamela Brauda 
# Professor: David Singletary
# College: Florida State College at Jacksonville
"""
Description: 
This is the Summer Working Connections Ohio 2025 - Credly Badge Criteria Project
There are 5 Items to complete and submit for a total grade of 100%.
This must achieve a minimum grade of 80%

The instructions are found on: https://github.com/FSCJ-FacultyDev/SWC_oHIo_2025 in the Assessment.ipynb file.

Note: Both professors are very knowledgeable and I would actually take a 16 week course with them and further increase my intelligence!
"""

# Item 2 - Login Security
from collections import defaultdict
from datetime import datetime

# track failed login attempts
login_attempts = defaultdict(int)

# lockout policy
MAX_ATTEMPTS = 3
LOG_FILE = "security_log.txt"

# security_log.txt will contain lockout entries
def log_event(message):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    with open(LOG_FILE, "a") as f:
        f.write(f"[{timestamp}] {message}\n")

# simulated login handler
def login(user, success):
    if login_attempts[user] >= MAX_ATTEMPTS:
        print(f"***Account for '{user}' is locked!***")
        log_event(f"LOCKOUT: {user} attempted login while locked.")
        return

    if success:
        print(f"{user} logged in successfully.")
        login_attempts[user] = 0  # Reset on success
    else:
        login_attempts[user] += 1
        print(f"Failed login attempt for {user} ({login_attempts[user]})")
        if login_attempts[user] >= MAX_ATTEMPTS:
            print(f"{user} has been locked out after {MAX_ATTEMPTS} failed attempts.")
            log_event(f"LOCKOUT: {user} locked out after {MAX_ATTEMPTS} failed attempts.")

