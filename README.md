# Premium Gold & Silver Calculator

A Vue.js application for calculating jewelry costs with precision. Calculate costs for gold and silver items based on rate, purity, weight, and making charges.

## Features

- Calculate costs for both gold and silver
- Adjust for purity levels (22k = 0.916, 24k = 1.000)
- Include making/design charges
- Automatic tax calculation (12%)
- Responsive design that works on all devices

## How to Use

1. Select the metal type (Gold or Silver)
2. Enter the rate per gram
3. Specify the purity (decimal format)
4. Enter the weight in grams
5. Add any design/making charges
6. Click "Calculate Total Cost" to see the breakdown

## Technical Details

- Built with Vue 3 Composition API
- Uses Vite for bundling
- Responsive CSS with gradient designs
- Deployed on Vercel

## Development

To run locally:
```bash
npm install
npm run dev
```

To build for production:
```bash
npm run build
```

## Deployment

This app is configured for deployment on Vercel. The `vercel.json` file includes rewrites for proper routing in a single-page application.