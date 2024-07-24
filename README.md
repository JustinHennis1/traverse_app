## Getting Started

These instructions will help you set up and run the project locally.

### Prerequisites

Before you begin, ensure you have the following installed:

- [Node.js](https://nodejs.org/) (v14 or higher)
- [npm](https://www.npmjs.com/) (comes with Node.js)

### Installation

1. **Clone the Repository**

   Clone the repository to your local machine using Git:

   ```bash
   git clone https://github.com/JustinHennis1/traverse_app.git

# Traverse

## The problem it solves
Traverse, our project for the 2024 Hackathon, aims to make going out with your friends a smoother and easier experience. Our goal was to create an app which would eliminate the question "...what next?" when out with your friends or visiting a new city. Traverse simplifies the travel planning process by enabling users to quickly create itineraries for both their local area and other cities across the US. It addresses the common frustration of filtering through numerous options for decent restaurants and activities. Users can effortlessly generate itineraries filled with top-rated and affordable activities with just the push of a button, allowing them to spend less time planning and more time enjoying their trip or outing. The platform allows users to select a state and city, and after searching, it displays the top tourist attractions in a list and on an interactive map. Airbnb listings are also integrated, with the best Airbnbs for the price and quality being prioritized, appearing on the bottom left of the screen for easy accommodation planning. Furthermore, Traverse offers deep insights into Airbnb data, analyzing top hosts and neighborhoods with violin plots, running regression models with an 80/20 train-test split, predicting prices based on independent variables, and visualizing listings on a heatmap. This comprehensive approach turns the cumbersome task of travel planning into a streamlined and enjoyable experience, providing all necessary tools and data in one convenient platform.


***
<details>
<summary>Traverse Preview</summary>
<br/>

# [Steps to Find Attractions and Accommodations in New York City using Traverse](https://app.tango.us/app/workflow/093b629c-fd46-4847-be82-449f0a068b7a?utm_source=markdown&utm_medium=markdown&utm_campaign=workflow%20export%20links)

## # [Traverse](http://localhost:5173/)
In this tutorial I will show the features of Traverse. A new travel planning app.


### 1. Select A State Within the US
![Step 1 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/802673ca-7076-44cb-be30-9704b37c2e68/d6dbd0e3-fd7c-4ae3-98dd-8cc28b1786d4.png?crop=focalpoint&fit=crop&fp-x=0.4305&fp-y=0.0701&fp-z=2.1611&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=389&mark-y=56&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz00MjImaD0xMTImZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 2. Select A City Belonging to That State
![Step 2 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/6fccc7a9-86ef-46e0-9e05-19299361880e/c7a56275-5a09-4679-9929-43c1040f8f80.png?crop=focalpoint&fit=crop&fp-x=0.6282&fp-y=0.0701&fp-z=2.2068&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=385&mark-y=57&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz00MzEmaD0xMTUmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 3. Click on Search
![Step 3 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/a84af3bf-ba05-46b0-a997-572181aa2704/6ede6e0b-a6c7-47ab-bde6-ea5b732c6ffb.png?crop=focalpoint&fit=crop&fp-x=0.7667&fp-y=0.0701&fp-z=2.6307&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=426&mark-y=59&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz0zNDgmaD0xNTYmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 4. Now you can view that city on the map
![Step 4 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/9b199fb6-c02f-4ebf-9a0e-6f69e3f124f2/88c0d4ef-d13f-4b06-a54b-2a28088a2609.png?crop=focalpoint&fit=crop&fp-x=0.1885&fp-y=0.5058&fp-z=1.1980&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=24&mark-y=68&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz00OTQmaD02MDQmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 5. As well as browse
![Step 5 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/94b97fff-e629-45ae-a011-75b4868fcfdf/d5fff90f-e8fa-4b22-a83b-77000bdf4f9b.png?crop=focalpoint&fit=crop&fp-x=0.6318&fp-y=0.3456&fp-z=1.9857&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=277&mark-y=240&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz02NDUmaD0yNjAmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 6. A list of local hotspots for dining, shopping and spending time
![Step 6 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/78c2cdf5-c26d-4e83-8f9a-3543cc7a4abb/87edc948-65a0-419d-8669-f07aee1efb0e.png?crop=focalpoint&fit=crop&fp-x=0.6782&fp-y=0.6093&fp-z=1.6486&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=37&mark-y=221&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz0xMTI3Jmg9Mjk3JmZpdD1jcm9wJmNvcm5lci1yYWRpdXM9MTA%3D)


### 7. Not Only Do We Provide Activities But Also Local Accommodations
![Step 7 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/b33fd17f-800f-4745-bff1-b669b2a30524/8edb56f6-f3fc-4a16-83dd-3bcdcc89ce77.png?crop=focalpoint&fit=crop&fp-x=0.1885&fp-y=0.7429&fp-z=1.5529&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=31&mark-y=408&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz02NDEmaD03MyZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 8. Click on a Listing  to View its Description
![Step 8 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/66bfede9-d37f-4b6d-abe0-fd42368010a9/ee8510d6-5132-4585-bff7-e2030f6be533.png?crop=focalpoint&fit=crop&fp-x=0.1874&fp-y=0.4958&fp-z=1.6647&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=74&mark-y=218&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz02MDEmaD0zMDQmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 9. Click on Close to Minimize Display…
![Step 9 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/c3efdaa6-dd83-4656-90dc-612b83ea0f10/0192ed21-0836-411a-a1dd-74164d40e17d.png?crop=focalpoint&fit=crop&fp-x=0.1874&fp-y=0.6110&fp-z=1.3311&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=26&mark-y=13&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz01NDYmaD03MTQmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 10. Moving On
![Step 10 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/5045b098-b595-4e57-bc3f-b71ac39a856b/36f08d2a-7ff5-44be-ae44-885a457d0385.png?crop=focalpoint&fit=crop&fp-x=0.1874&fp-y=0.1970&fp-z=1.5578&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=31&mark-y=191&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz02MzkmaD03MyZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 11. Click on Nearby Search to view Local Attractions
![Step 11 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/683820dc-35e5-4904-bae5-9d3ee8b6ee34/591c4e65-375f-4bd4-b98a-4ffe7742afc2.png?crop=focalpoint&fit=crop&fp-x=0.9037&fp-y=0.0701&fp-z=2.6307&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=644&mark-y=59&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz01MDQmaD0xNTYmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 12. It may take some time to load
![Step 12 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/26fa926c-6d58-4bf3-85e5-19b02954391c/0cf73ef9-47c4-4f9c-89ef-311ade276bbf.png?crop=focalpoint&fit=crop&fp-x=0.4995&fp-y=0.5693&fp-z=2.5852&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=517&mark-y=287&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz0xNjYmaD0xNjYmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 13. Voila... Your Local Activities and Restaurants are Now Available
![Step 13 screenshot](https://images.tango.us/workflows/093b629c-fd46-4847-be82-449f0a068b7a/steps/ada4db0b-afa7-438d-97bf-705cbcf0e02e/38f826e6-08e6-40e4-8bcd-00aee5bfcb3b.png?crop=focalpoint&fit=crop&fp-x=0.1885&fp-y=0.5058&fp-z=1.1980&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=24&mark-y=68&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz00OTQmaD02MDQmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)
