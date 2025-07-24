import React, { useState } from 'react';
import axios from 'axios';

function RegexSearch() {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);
  const [fallback, setFallback] = useState([]);
  const [message, setMessage] = useState('');
  const [error, setError] = useState('');

  const handleSearch = async (e) => {
    e.preventDefault();
    setResults([]);
    setFallback([]);
    setMessage('');
    setError('');

    try {
      const res = await axios.post('http://127.0.0.1:5000/api/search', { query });
      setResults(res.data.results);
      setFallback(res.data.fallback);
      setMessage(res.data.fallback_message);
    } catch (err) {
      setError('Search failed. Make sure your backend is running and CORS is enabled.');
    }
  };

  return (
    <div>
      <form onSubmit={handleSearch} style={{ marginBottom: '1rem' }}>
        <input
          type="text"
          placeholder="Enter regex query"
          value={query}
          onChange={(e) => setQuery(e.target.value)}
          required
        />
        <button type="submit">Search</button>
      </form>

      {error && <p style={{ color: 'red' }}>{error}</p>}

      {results.length > 0 && (
        <div>
          <h2>Search Results</h2>
          <ul>
            {results.map((movie, index) => (
              <li key={index}>
                <strong>{movie.title}</strong> ({movie.release_year})<br />
                <em>{movie.genres.join(', ')}</em><br />
                Cast: {movie.cast.join(', ')}<br />
                Director: {movie.director}<br />
                Plot: {movie.plot}
              </li>
            ))}
          </ul>
        </div>
      )}

      {fallback.length > 0 && (
        <div>
          <h3>{message}</h3>
          <ul>
            {fallback.map((movie, index) => (
              <li key={index}>
                <strong>{movie.title}</strong> (Director: {movie.director})<br />
                Cast: {movie.cast.join(', ')}
              </li>
            ))}
          </ul>
        </div>
      )}
    </div>
  );
}

export default RegexSearch;
