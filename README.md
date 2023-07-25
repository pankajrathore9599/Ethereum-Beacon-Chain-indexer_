For this Ethereum Beacon Chain indexer project, we can implement a layered architecture that organizes your code into layers each having a specific role. Here's an outline:

Data Access Layer: This layer is responsible for communicating with your database. It will contain functions to save and retrieve the participation rate of validators from the PostgreSQL database. In Rust, you'll use Diesel for this.

Beacon Chain Interface Layer: This layer communicates with the Ethereum Beacon Chain. It retrieves information about epochs and validators. You will use the web3 library to connect to and fetch data from the Beacon Chain.

Service Layer: This layer acts as the glue between the data access layer and the Beacon Chain interface layer. It contains the core logic of your application, namely, the calculation of the participation rate and the indexing of epochs. This is where the interaction between the retrieved beacon chain data and the PostgreSQL database takes place.

API Layer: This is the topmost layer that exposes REST APIs to query the indexed data. It will use Rocket to define endpoints where users can query participation rates. It takes the user requests, passes them to the service layer, and formats the responses to be sent back to the user.

|---------------------|       |------------------------|  
|     API Layer       |       |       Client           |
|---------------------|       |------------------------|
           ^                             |
           |                             V
|---------------------|      Query       |------------------------|
|     Service Layer   |<---------------->|    Beacon Chain Layer  |
|---------------------|                  |------------------------|
           ^                             |
           |                             V
|---------------------|      Query/Update |------------------------|
|  Data Access Layer  |<---------------->|       Database         |
|---------------------|                  |------------------------|

