# android-check-internet-connection

```java
    private fun isConnectedToInternet(): Boolean {
        val connectivityManager = getSystemService(Context.CONNECTIVITY_SERVICE) as ConnectivityManager
        return if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
            isConnectedForAndroid23AndAbove(connectivityManager)
        else
            isConnectedUnderAndroid23(connectivityManager)
    }

    @RequiresApi(Build.VERSION_CODES.M)
    private fun isConnectedForAndroid23AndAbove(connectivityManager: ConnectivityManager): Boolean {
        val capabilities = connectivityManager.getNetworkCapabilities(connectivityManager.activeNetwork)
        return capabilities?.run {
            capabilities.hasTransport(NetworkCapabilities.TRANSPORT_WIFI) || capabilities.hasTransport(NetworkCapabilities.TRANSPORT_CELLULAR)
        } ?: false
    }

    @Suppress("DEPRECATION")
    private fun isConnectedUnderAndroid23(connectivityManager: ConnectivityManager): Boolean {
        return connectivityManager.activeNetworkInfo?.run {
            type == ConnectivityManager.TYPE_WIFI || type == ConnectivityManager.TYPE_MOBILE
        } ?: false
    }
```
