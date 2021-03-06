**Info**
----
Movie API allow you to add new movie and get random movie.

You can find extended version (CRUD) on branch `dev`

**How to run:**
----
1. `yarn install` 
2. `yarn build`
3. `yarn start` // x2 if app-config.json does not exists

### How run tests:
1. Unit: 
- `yarn test:unit`

2. API:
- `yarn start:testing`
- open new terminal
- `yarn test:api`


**Movie API**
----

#### Get random movie/s:
It return rondom movie/s. You can specify optional search parameters: `duration`, `genres`. 

* **URL** `/movie/random`

* **Method:** `POST` 
  
*  **Data params:**

   **Optional:**
 
   `duration=[integer]`
   
   `duration=[array of string]`
   
   **Sample body:**
   ```json
   { 
      "duration": 120,
      "genres": ["Action", "Comedy"]
   }  
   ```
   
* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
    ```json
    [ 
      { 
          "id": 2,
          "title": "Title",
          "year": 1911,
          "runtime": 116,
          "director": "Tester Test",
          "actors": "",
          "plot": "",
          "posterUrl": "",
          "genres": [ "Action", "Comedy" ] 
      },
      { 
          "id": 3,
          "title": "Title 2",
          "year": 2012,
          "runtime": 121,
          "director": "Tester Test Jr",
          "actors": "",
          "plot": "",
          "posterUrl": "",
          "genres": [ "Sci-Fi", "Comedy" ] 
      }
     
    ]
    ``` 
* **Error Response:**

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{ message: 'Invalid duration type. Required number' }`

  OR
  
    * **Code:** 400 BAD REQUEST <br />
      **Content:** `{ message: 'Invalid geners type. Required array of string' }`
  
    OR

  * **Code:** 500 SERVER ERROR <br />
    **Content:** `{ message : "Something goes wrong" }`

* **Sample Call:**

    ```javascript
      $.ajax({
        url: "/movie/random",
        dataType: "json",
        type : "POST",
        data: JSON.stringify({
          genres: ["Action", "horror"],
        }),
        success : function(r) {
          console.log(r);
        }
      });
    ```
  
 ----
 
#### Add movie:
Request add new movie.
 
 * **URL** `/movie`
 
 * **Method:** `POST` 
   
 *  **Data params:**
 
    **Required:**
 
       `title=[string], (max 255 characters)`
       
       `year=[integer]`
       
       `runtime=[integer]`
       
       `director=[string], (max 255 characters)`
       
       `genres=[array of string], (min 1)`
       
    **Optional:**
    
       `actors=[string]`
       
       `id=[number]` // auto generated
       
       `plot=[string]`
       
       `posterUrl=[string]`
       
    **Sample body:**
    ```json
    { 
       "title" : "Awesome Movie 3",
       "runtime": 86,
       "year": 1986,
       "genres": ["Comedy"],
       "director": "Jan Kowalsky",
       "posterUrl": "https://poster.com/awesome_movie_3"
    }  
    ```
    
 * **Success Response:**
 
   * **Code:** 200 <br />
     **Content:** 
     ```json
     {
       "id" : 123
     }
     ``` 
 * **Error Response:**
 
   * **Code:** 400 BAD REQUEST <br />
     **Content:** `{ message: '<validation message>' }`
 
   OR
   
     * **Code:** 400 BAD REQUEST <br />
       **Content:** `{ message: 'Movie with id 123 arleady exist' }`
   
     OR
 
   * **Code:** 500 SERVER ERROR <br />
     **Content:** `{ message : "Something goes wrong" }`
 
 * **Sample Call:**
 
     ```javascript
       $.ajax({
         url: "/movie",
         dataType: "json",
         type : "POST",
         data: JSON.stringify(
               { 
                  "title" : "Awesome Movie 3",
                  "runtime": 86,
                  "year": 1986,
                  "genres": ["Comedy"],
                  "director": "Jan Kowalsky",
                  "posterUrl": "https://poster.com/awesome_movie_3"
               }     
         ),
         success : function(r) {
           console.log(r);
         }
       });
     ```
