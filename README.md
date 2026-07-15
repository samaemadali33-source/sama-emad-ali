// Step 1: Define the function
function isValidEmail(email) {
  // Step 2 & 3: Create and refine a Regex pattern
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/i;
  
  // Step 4: Use test() method
  // Step 5: Return the result
  return emailRegex.test(email);
}

// Step 6 & 7: Test your function with sample emails and edge cases
console.log('isValidEmail("test@example.com") →', isValidEmail("test@example.com"));
console.log('isValidEmail("invalid-email") →', isValidEmail("invalid-email"));
console.log('isValidEmail("user@domain.co") →', isValidEmail("user@domain.co"));
console.log('isValidEmail("missing@domain") →', isValidEmail("missing@domain"));
console.log('isValidEmail("@nodomain.com") →', isValidEmail("@nodomain.com"));
console.log('isValidEmail("two@@at.com") →', isValidEmail("two@@at.com"));
console.log('isValidEmail("spaced @email.com") →', isValidEmail("spaced @email.com"));
