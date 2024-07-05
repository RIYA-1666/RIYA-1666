
import re

def assess_password_strength(password):
    # Criteria
    length_criteria = len(password) >= 8
    uppercase_criteria = bool(re.search(r'[A-Z]', password))
    lowercase_criteria = bool(re.search(r'[a-z]', password))
    digit_criteria = bool(re.search(r'\d', password))
    special_char_criteria = bool(re.search(r'[@$!%*?&#]', password))

    # Assessing the strength
    strength = 0
    feedback = []

    if length_criteria:
        strength += 1
    else:
        feedback.append("Password should be at least 8 characters long.")

    if uppercase_criteria:
        strength += 1
    else:
        feedback.append("Password should include at least one uppercase letter.")

    if lowercase_criteria:
        strength += 1
    else:
        feedback.append("Password should include at least one lowercase letter.")

    if digit_criteria:
        strength += 1
    else:
        feedback.append("Password should include at least one digit.")

    if special_char_criteria:
        strength += 1
    else:
        feedback.append("Password should include at least one special character (@$!%*?&#).")

    # Strength feedback
    if strength == 5:
        feedback.append("Password is very strong.")
    elif strength >= 3:
        feedback.append("Password is strong.")
    elif strength >= 2:
        feedback.append("Password is medium.")
    else:
        feedback.append("Password is weak.")

    return strength, feedback

# Example usage
password = input("Enter a password to assess: ")
strength, feedback = assess_password_strength(password)

print(f"Password strength: {strength}/5")
print("Feedback:")
for comment in feedback:
    print(f"- {comment}")
