# Part 6 — Starter

This part builds on your **Part 5** solution. The key goals are to
1. load the sonnets from the PoetryDB server instead of using a local file
2. cache the sonnets locally for speed and resource savings (most importantly, your time ⏱️)
3. add timing to be able to observe how execution speed varies

## Run the app

```bash
python -m part6.app
```

## What to implement (ToDos)

As always, your todos are located in `app.py`, specifically, in `part6/app.py`

0. **Copy** your implementation from part 5: reading and writing `config.json`.
1. **Remote data source (PoetryDB)**  
   Load Shakespeare's sonnets from the PoetryDB API. The endpoint which returns all sonnets in JSON format is:
   `https://poetrydb.org/author,title/Shakespeare;Sonnet`

2. **Caching**

   You'll notice that loading the sonnet JSON file from the PoertyDB server takes several seconds.
   To avoid repeated API calls and save resources:
   - Cache the downloaded sonnets into a local JSON file (e.g. `part6/sonnets.json`).
   - On subsequent runs, load from this cache instead of calling the API again.
   - To make this robust, check whether the cache file already exists in your project folder before downloading.

3. **Timing**
   
   Another aspect of part 6 is measuring execution time - typically by recording time differences. 
   Here is an example:
    ```python
    import time
    
    start = time.perf_counter()
    # The code you want to measure here
    end = time.perf_counter()
    
    elapsed = (end - start) * 1000
    print(f"Elapsed time: {elapsed:.3f} [ms]")
    ```
   - Measure and print the following timings to the console:
     - When loading the sonnets: Print whether they were loaded from **cache** or **API** and how long it took (in milliseconds).
     - When evaluating a user query: Print how long the query took, e.g.  
         `1 out of 3 sonnets contain "love summer". Your query took 3.12ms.`

## Implementation hints

- Use `urllib.request` from the standard library for the HTTP request.
- Use `time.perf_counter()` for timing (high-resolution).
- Make sure your query timing only covers the search work, **not** user input.
