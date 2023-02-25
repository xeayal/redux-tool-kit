# createAsyncThunk - Redux Toolkit | createAsyncThunk ile API isteği nasıl yapılır?

Redux Toolkit içinde createAsyncThunk fonksiyonu, asenkron bir işlem yapmak için kullanabileceğiniz bir işlevdir. Aşağıdaki örnekte, bir kullanıcının adını almak için bir API çağrısı yapmak için kullanılmaktadır:

```javascript
import { createAsyncThunk } from '@reduxjs/toolkit';
import axios from 'axios';

export const fetchUser = createAsyncThunk('users/fetchUser', async (name) => {
  const response = await axios.get(`https://api.example.com/users/${name}`);
  return response.data;
});
```
Bu işlev, users/fetchUser türünde bir aksiyon oluşturur ve geri dönüş değeri olarak API'den dönen verileri döndürür. Bu işlevi kullanmak için, bir users reducer'ı oluşturmanız ve bu aksiyonu işlemek için case eklemeniz gerekir:

```javascript
import { createSlice } from '@reduxjs/toolkit';
import { fetchUser } from './usersSlice';

const usersSlice = createSlice({
  name: 'users',
  initialState: [],
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(fetchUser.pending, (state) => {
        // Handle the loading state
      })
      .addCase(fetchUser.fulfilled, (state, action) => {
        // Handle the success state
        state.push(action.payload);
      })
      .addCase(fetchUser.rejected, (state, action) => {
        // Handle the error state
      });
  },
});
```
Bu örnekte, fetchUser işlevi çağrıldığında, users/fetchUser_pending, users/fetchUser_fulfilled, veya users/fetchUser_rejected türünde aksiyonlar oluşur ve bunları işlemek için extraReducers kullanılmaktadır.
