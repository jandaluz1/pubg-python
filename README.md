# pubg-python

A python wrapper for the PUBG developer API

[PUBG Developer API Official Documentation](https://developer.playbattlegrounds.com/docs/en/introduction.html)

*This is a MVP and the package is currently under development, please feel free to contribute*

*Initial version still needs to be uploaded to PyPI*

## Usage

### Specifying a shard

The PUBG API shards data by platform and region, and therefore requires a shard to be specified in the URL for most requests.

```python
from pubg_python import PUBG, Shard

api = PUBG('<api-key>', Shard.PC_NA)
```

A list of shards can be found [here](https://developer.playbattlegrounds.com/docs/en/making-requests.html#regions) and the wrapper constants [here](https://github.com/ramonsaraiva/pubg-python/blob/master/pubg_python/base.py)

## Retrieving a list of matches

Retrieving a list of matches is as simple as this:

```python
matches = api.matches()
```

## Retrieving a single match

Retrieving a single match is also a piece of cake:

```python
match = api.matches().get(12345)
```

### Limits and Offsets

Offsetting 5 matches and limitting by 10

```python
matches = api.matches().limit(10).offset(5)
```

### Sorting

`sort` defaults to ascending, you can use `ascending=False` for a descending sort

```python
matches = api.matches().limit(10).sort('createdAt')
matches = api.matches().limit(10).sort('createdAt', ascending=False)
```

### Filtering

Applying a `gameMode` filter: [you can check all available filters here](https://developer.playbattlegrounds.com/docs/en/matches.html#/Matches/get_matches)

```python
squad_matches = api.matches().filter('gameMode', 'squad')
```

### Pagination

Use `next()` for the next page and `prev()` for the previous one:

```python
matches = api.matches()
next_matches = matches.next()
previous_matches = matches.prev()
```

### I want them all!

Be aware of rate limits:

```python
matches = api.matches()
while matches:
    for match in matches:
        print(match)
    matches = matches.next()
```