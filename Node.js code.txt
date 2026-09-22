const API_URL = "https://jsonplaceholder.typicode.com/users";

async function fetchUsers() {
    try {
        // Fetch user data from API
        const response = await fetch(API_URL);

        // Convert response into JSON
        const users = await response.json();

        // Filter users whose catchPhrase contains "group" or "service"
        const filteredUsers = users.filter(user =>
            user.company.catchPhrase.toLowerCase().includes("group") ||
            user.company.catchPhrase.toLowerCase().includes("service")
        );

        // Transform data using Object Destructuring
        const formattedUsers = filteredUsers.map(
            ({ name, email, address: { city } }) =>
                `User: ${name} | Email: ${email} | City: ${city}`
        );

        // Display result
        console.log(formattedUsers);

    } catch (error) {
        console.error("Error fetching users:", error);
    }
}

fetchUsers();