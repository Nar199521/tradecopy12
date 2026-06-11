# Real Forex Data Setup Guide

## 🚀 Getting Started with Live Forex Rates

Your app now uses **real live forex data** from Alpha Vantage API with charts and real-time rates for all major currency pairs.

### ✅ What's New

1. **Real Forex Rates** - All major currency pairs (EURUSD, GBPUSD, USDJPY, etc.)
2. **Live Charts** - Interactive area charts with open/high/low/close data
3. **Real-time Updates** - Rates refresh every 60 seconds
4. **Multiple Intervals** - View 15-minute intraday or daily charts

### 🔑 API Setup (2 minutes)

#### Step 1: Get Free API Key
1. Visit: https://www.alphavantage.co/api/
2. Fill out the form (takes 1 minute)
3. Check your email for the API key
4. Keep it handy!

#### Step 2: Add to .env.local
Create or update `.env.local` in your project root:

```env
ALPHA_VANTAGE_API_KEY=your_api_key_here
```

Replace `your_api_key_here` with your actual API key from step 1.

#### Step 3: Restart Dev Server
```bash
npm run dev
```

Your dashboard will now show:
- ✅ Real forex rates for all major pairs
- ✅ Interactive charts with price history
- ✅ Bid/Ask spreads
- ✅ Trend indicators (up/down)

### 📊 Free Tier Limits
- **5 requests/minute** - Plenty for your dashboard
- **500 requests/day** - More than enough
- **Real-time updates** - Rates auto-refresh

### 🎯 Features

#### Forex Rates Panel
- Click on any pair to view its chart
- Toggle between 15-minute (intraday) and daily intervals
- View bid/ask spreads
- See percentage change
- Real-time auto-refresh every 60 seconds

#### API Endpoints
```bash
# Get all major forex rates
curl "http://localhost:3000/api/forex"

# Get specific pair
curl "http://localhost:3000/api/forex?pair=EURUSD"

# Get chart data (15-minute)
curl "http://localhost:3000/api/forex/chart?pair=EURUSD&interval=intraday"

# Get chart data (daily)
curl "http://localhost:3000/api/forex/chart?pair=EURUSD&interval=daily"
```

### 🔧 Troubleshooting

**"Failed to fetch rate"** error?
- Check API key is set in `.env.local`
- Verify you have internet connection
- Check Alpha Vantage API status
- Wait 1 minute - API has rate limits

**No chart data showing?**
- Alpha Vantage free tier has strict rate limits
- Try again after a minute
- First time may take longer to fetch history

**Want unlimited requests?**
- Alpha Vantage paid tier: $20-50/month
- Or use alternative: Twelve Data, Finnhub

### 📈 Next Steps

1. ✅ Add your API key to `.env.local`
2. ✅ Restart dev server
3. ✅ Visit http://localhost:3000
4. ✅ See live forex rates!

### 🎨 Customization

To add more currency pairs, edit `src/lib/forex-service.ts`:

```typescript
export const MAJOR_FOREX_PAIRS = [
  'EURUSD',  // EUR/USD
  'GBPUSD',  // GBP/USD
  'USDJPY',  // USD/JPY
  'AUDUSD',  // AUD/USD
  // Add more here
];
```

---

**Questions?** Check Alpha Vantage docs at https://www.alphavantage.co/documentation/
