```javascript
import { createAsyncThunk } from '@reduxjs/toolkit';
import axios from 'axios';

export const fetchUser = createAsyncThunk('users/fetchUser', async (name) => {
  const response = await axios.get(`https://api.example.com/users/${name}`);
  return response.data;
});
```
