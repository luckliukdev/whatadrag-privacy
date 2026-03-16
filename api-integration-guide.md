# API Integration Guide

## Submitting Scores from Games

To submit scores from your games, you need to send a POST request to the endpoint `https://api.whatadrag.com/scores` with the following JSON payload:

```json
{
    "playerId": "string",
    "gameId": "string",
    "score": integer
}
```

### Example Code (JavaScript)

```javascript
const submitScore = async (playerId, gameId, score) => {
    const response = await fetch('https://api.whatadrag.com/scores', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
        },
        body: JSON.stringify({ playerId, gameId, score })
    });
    const data = await response.json();
    return data;
};
```

## Proper Error Handling

When submitting scores, your request may fail due to various reasons. Make sure to handle errors appropriately:

1. **Network Errors**: Implement retries or catch network-related errors.
2. **API Errors**: Check the HTTP status code and handle errors accordingly.

### Example Error Handling

```javascript
try {
    const result = await submitScore(playerId, gameId, score);
    console.log('Score submitted successfully:', result);
} catch (error) {
    console.error('Error submitting score:', error);
}
```

## Validation Requirements for Level >= 50

Players must have a level of 50 or higher to submit scores. Check the player's level before submission:

### Example Validation Check

```javascript
if (playerLevel >= 50) {
    await submitScore(playerId, gameId, score);
} else {
    console.error('Player level must be 50 or higher to submit scores.');
}
```

## Token Setup Instructions

1. Visit [API Tokens page](https://api.whatadrag.com/tokens).
2. Click on *Create New Token*.
3. Note down your token securely.
4. Use the token in your API requests in the header as shown above.

## Troubleshooting Guide

- **Error Code 401**: Unauthorized – Check if your token is valid or expired.

- **Error Code 422**: Unprocessable Entity – Verify that the payload meets the requirements (valid player ID, game ID, and score).

- **Error Code 500**: Internal Server Error – Try again later; this may be a temporary issue with the API.

For more help, contact support at support@whatadrag.com.