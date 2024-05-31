This project is a travel tracker called that helps students choose travel destinnations, play games, etc. By working on this project, I gained valuable information on backend and frontend development and connectivity, along with teamwork.

Students can create accounts and login with the same account credentials. This is done in order to allow independent tracking of college applications, creating a highly personalized experience. The creation of the account is done using a POST method in the API endpoint /api/users. These credentials are stored in the backend in an SQLite database, and are fetched using the GET method under the same endpoint.

Upon logging in, the student is redirected to the Travel home page. These features work using a PUT method under the API endpint /api/users/. 

IMPORTANT: The travel elements are saved as a list, and are fetched using this code line: json.loads(user.travel_list). This list is saved in the SQLite database, and is unique to each user.

