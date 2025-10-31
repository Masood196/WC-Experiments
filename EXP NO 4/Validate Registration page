<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Registration Validation</title>

    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        
        body {
            font-family: "Inter", sans-serif;
            background-color: #f7fafc;
        }
        .form-control {
            transition: all 0.3s ease;
        }
        .form-control:focus {
            border-color: #4c51bf; /* Indigo focus ring */
            box-shadow: 0 0 0 3px rgba(76, 81, 191, 0.5);
            outline: none;
        }
        .error-message {
            opacity: 0;
            height: 0;
            overflow: hidden;
            transition: opacity 0.3s ease, height 0.3s ease;
        }
        .error-message.visible {
            opacity: 1;
            height: auto;
            margin-top: 4px;
        }
    </style>
</head>
<body class="flex items-center justify-center min-h-screen p-4">

    <div class="w-full max-w-lg bg-white p-8 md:p-10 rounded-xl shadow-2xl">
        <h1 class="text-3xl font-extrabold text-gray-900 mb-6 text-center">
            Register Account
        </h1>

        <form id="registrationForm" onsubmit="return validateForm(event)" novalidate>

            <!-- Username Field -->
            <div class="mb-5">
                <label for="username" class="block text-sm font-medium text-gray-700 mb-1">Username</label>
                <input type="text" id="username" name="username" placeholder="Enter your desired username"
                       class="form-control w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-indigo-500 focus:border-indigo-500">
                <p id="usernameError" class="error-message text-xs text-red-500"></p>
            </div>

            <!-- Email Field -->
            <div class="mb-5">
                <label for="email" class="block text-sm font-medium text-gray-700 mb-1">Email Address</label>
                <input type="email" id="email" name="email" placeholder="you@example.com"
                       class="form-control w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-indigo-500 focus:border-indigo-500">
                <p id="emailError" class="error-message text-xs text-red-500"></p>
            </div>

            <!-- Password Field -->
            <div class="mb-5">
                <label for="password" class="block text-sm font-medium text-gray-700 mb-1">Password</label>
                <input type="password" id="password" name="password" placeholder="Minimum 8 characters"
                       class="form-control w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-indigo-500 focus:border-indigo-500">
                <p id="passwordError" class="error-message text-xs text-red-500"></p>
            </div>

            <!-- Confirm Password Field -->
            <div class="mb-6">
                <label for="confirmPassword" class="block text-sm font-medium text-gray-700 mb-1">Confirm Password</label>
                <input type="password" id="confirmPassword" name="confirmPassword" placeholder="Re-enter your password"
                       class="form-control w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-indigo-500 focus:border-indigo-500">
                <p id="confirmPasswordError" class="error-message text-xs text-red-500"></p>
            </div>

            <!-- Terms & Conditions Checkbox -->
            <div class="mb-6 flex items-start">
                <input type="checkbox" id="terms" name="terms"
                       class="h-4 w-4 text-indigo-600 border-gray-300 rounded focus:ring-indigo-500 mt-1">
                <label for="terms" class="ml-2 text-sm text-gray-900 select-none">
                    I agree to the <a href="#" class="text-indigo-600 hover:text-indigo-500 font-medium">Terms and Conditions</a>
                </label>
            </div>
            <p id="termsError" class="error-message text-xs text-red-500 -mt-2 mb-4"></p>


            <!-- Submit Button -->
            <button type="submit"
                    class="w-full flex justify-center py-3 px-4 border border-transparent rounded-lg shadow-sm text-sm font-medium text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition duration-150 ease-in-out">
                Create Account
            </button>
        </form>

        <!-- General Message Box (for success/failure) -->
        <div id="generalMessage" class="mt-6 p-3 rounded-lg text-sm text-center hidden" role="alert"></div>

    </div>

    <script>
        /**
         * Clears the error message for a specific field.
         * @param {string} fieldId - The ID of the form field.
         */
        function clearError(fieldId) {
            const errorElement = document.getElementById(fieldId + 'Error');
            const inputElement = document.getElementById(fieldId);

            if (errorElement) {
                errorElement.textContent = '';
                errorElement.classList.remove('visible');
            }
            if (inputElement) {
                inputElement.classList.remove('border-red-500');
                inputElement.classList.add('border-gray-300');
            }
        }

        /**
         * Displays the error message for a specific field.
         * @param {string} fieldId - The ID of the form field.
         * @param {string} message - The error message to display.
         */
        function displayError(fieldId, message) {
            const errorElement = document.getElementById(fieldId + 'Error');
            const inputElement = document.getElementById(fieldId);

            if (errorElement) {
                errorElement.textContent = message;
                errorElement.classList.add('visible');
            }
            if (inputElement) {
                inputElement.classList.remove('border-gray-300');
                inputElement.classList.add('border-red-500');
            }
        }

        /**
         * Displays a general success or failure message at the bottom of the form.
         * @param {string} message - The message content.
         * @param {string} type - 'success' or 'failure'.
         */
        function displayGeneralMessage(message, type) {
            const msgBox = document.getElementById('generalMessage');
            msgBox.textContent = message;
            msgBox.classList.remove('hidden', 'bg-red-100', 'text-red-700', 'bg-green-100', 'text-green-700');

            if (type === 'success') {
                msgBox.classList.add('bg-green-100', 'text-green-700');
            } else if (type === 'failure') {
                msgBox.classList.add('bg-red-100', 'text-red-700');
            }

            // Hide the message after 5 seconds
            setTimeout(() => {
                msgBox.classList.add('hidden');
            }, 5000);
        }

        /**
         * Validates the entire registration form.
         * @param {Event} event - The form submission event.
         * @returns {boolean} - True if validation passes, false otherwise.
         */
        function validateForm(event) {
            event.preventDefault(); // Stop the form from submitting by default
            let isValid = true;

            // Clear all previous errors
            ['username', 'email', 'password', 'confirmPassword', 'terms'].forEach(clearError);

            const username = document.getElementById('username').value.trim();
            const email = document.getElementById('email').value.trim();
            const password = document.getElementById('password').value;
            const confirmPassword = document.getElementById('confirmPassword').value;
            const termsChecked = document.getElementById('terms').checked;

            // --- 1. Username Validation ---
            if (username === '') {
                displayError('username', 'Username is required.');
                isValid = false;
            } else if (username.length < 3) {
                displayError('username', 'Username must be at least 3 characters long.');
                isValid = false;
            }

            // --- 2. Email Validation ---
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (email === '') {
                displayError('email', 'Email address is required.');
                isValid = false;
            } else if (!emailRegex.test(email)) {
                displayError('email', 'Please enter a valid email address (e.g., user@domain.com).');
                isValid = false;
            }

            // --- 3. Password Validation ---
            // Requires: min 8 chars, 1 uppercase, 1 lowercase, 1 number, 1 special char
            const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/;
            if (password === '') {
                displayError('password', 'Password is required.');
                isValid = false;
            } else if (!passwordRegex.test(password)) {
                displayError('password', 'Password must be 8+ chars, incl. uppercase, lowercase, number, and special char (@$!%*?&).');
                isValid = false;
            }

            // --- 4. Confirm Password Validation ---
            if (confirmPassword === '') {
                displayError('confirmPassword', 'Confirming the password is required.');
                isValid = false;
            } else if (password !== confirmPassword) {
                displayError('confirmPassword', 'Passwords do not match.');
                isValid = false;
            }

            // --- 5. Terms & Conditions Validation ---
            if (!termsChecked) {
                displayError('terms', 'You must agree to the Terms and Conditions.');
                isValid = false;
            }

            // --- Final Submission ---
            if (isValid) {
                // If validation passes, simulate form submission success
                displayGeneralMessage('Registration successful! Redirecting to dashboard...', 'success');
                // In a real application, you would now send data to the server via fetch or XMLHttpRequest
                console.log('Form data ready to be submitted:', { username, email, password });
                
                // Clear the form (optional)
                document.getElementById('registrationForm').reset();
            } else {
                // If validation fails, display a general failure notice
                displayGeneralMessage('Please correct the errors marked in red.', 'failure');
            }

            return isValid;
        }
    </script>
</body>
</html>
