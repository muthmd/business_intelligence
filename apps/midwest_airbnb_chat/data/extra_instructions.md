# Extra Instructions

Rules the LLM follows when it writes SQL for `listings`.

- `price` is the nightly price in U.S. dollars. When the user asks what something costs, use `price` and round money to whole dollars in the answer.
- `host_is_superhost` is text, not a boolean: superhosts have `host_is_superhost = 't'` and other hosts have `host_is_superhost = 'f'`.
- Match cities with `city = 'Chicago'`, `city = 'Columbus'`, or `city = 'Twin Cities'`. "Minneapolis" or "St. Paul" means `city = 'Twin Cities'`.
- Search `name` case-insensitively with `LOWER(name) LIKE '%term%'`.
- When averaging ratings, ignore rows where `review_scores_rating` is `NULL`.
- "Entire homes" means `room_type = 'Entire home/apt'`, and a question about fitting a number of people (for example "a party of ten") means `accommodates >=` that number.