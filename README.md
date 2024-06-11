# Movie Recommendation 

This is a simple workflow with Weaviate and Cohere, using Movielens dataset.

It's a movie recommendation system: if you don't know what to watch tonight you can provide
a title of a movie that you like or just search for some keywords (tags).

In both cases the system will suggest you two movies with a short description.

## Requirements

- Python >3.7
- Following python libraries:
  - `weaviate-client`
  - `python-dotenv`
- A Weaviate cluster on Weaviate Cloud (URL and API KEY).
- An API KEY for Cohere.

## Installation

1. Clone the repository.

2. Create a virtual environment 

    ```bash
    python -m venv venv
    source venv/bin/activate
    ```

3. Install dependencies:

    ```bash
    pip install weaviate-client python-dotenv
    ```

4. Create an `.env` file in the project directory and add your API keys and WCD URL:

    ```env
    WCD_URL=your_weaviate_cluster_url
    WCD_API_KEY=your_weaviate_api_key
    COHERE_APIKEY=your_cohere_api_key
    ```

## Data management

 _manage\_data.ipynb_ it's where the preparation of the movie dataset and the uploading of the collection on Weaviate cloud are managed. I decided to use named vectors for title and tags since the queries are made on one of these two fields.
 Binary quantization is used for reducing the size of the data.

## Usage

0. Load the data on your Weaviate cloud with _manage\.data.ipynb_.
1. Run _GUI.ipynb_ (it's vintage not ugly)
2. Choose if you want to search by title or by tag.
3. You will see two movies recommendations with a short description done with Cohere.

## Recommendations

How it works? 
The recommendations are made with tags. If you input a movie title, the system will retrieve the tags for that title from Weaviate database and search for the movies with most similar tags. Or you can directly input some tags that you find interesting.

Both movie titles and tags are vectorized indipendently in the Weaviate database, the searches are done with vector similarity, adding the generative search that passes the results to prompt an LLM (Cohere).


## Disclaimer

This is an exercise for a challenge, not intended for general user usage. 