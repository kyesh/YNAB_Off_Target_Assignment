# YNAB Off-Target Assignment Analysis

A comprehensive Next.js web application that integrates with the YNAB API to analyze budget target alignment, helping users understand how their monthly budget assignments compare against their predefined targets.

![YNAB Analysis Dashboard](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)
![Next.js](https://img.shields.io/badge/Next.js-14+-black)
![TypeScript](https://img.shields.io/badge/TypeScript-5.4+-blue)
![React](https://img.shields.io/badge/React-18+-blue)

## 🎯 What This Application Does

This tool provides **detailed budget analysis** for YNAB users by:

- **Calculating "Needed This Month"** values using 7 sophisticated rules that mirror YNAB's internal logic
- **Analyzing target alignment** to show which categories are over-target, under-target, or on-target
- **Providing comprehensive debugging UI** with detailed calculation breakdowns and rule explanations
- **Offering variance analysis** with dollar amounts and percentage calculations
- **Supporting all YNAB goal types** including monthly, weekly, target balance, and months-to-budget goals

### Key Features

✅ **Smart Calculation Engine**: 7-rule system handles all YNAB goal types accurately  
✅ **Interactive Debug UI**: See exactly how each calculation is performed  
✅ **Monthly Overview**: Income, activity, budgeted amounts, and variance summaries  
✅ **Category Analysis**: Detailed breakdown of over/under-target categories  
✅ **Real-time Data**: Direct integration with YNAB API v1  
✅ **Responsive Design**: Works on desktop, tablet, and mobile devices  

## 🚀 Quick Start

### Prerequisites

- **Node.js 18+** and npm 8+
- **YNAB account** with budget data
- **YNAB Personal Access Token** ([Get yours here](https://app.ynab.com/settings/developer))

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/YNAB_Off_Target_Assignment.git
   cd YNAB_Off_Target_Assignment
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure environment**
   ```bash
   cp .env.example .env.local
   ```
   
   Edit `.env.local` and add your YNAB Personal Access Token:
   ```env
   YNAB_ACCESS_TOKEN=your-ynab-personal-access-token-here
   ```

4. **Start development server**
   ```bash
   npm run dev
   ```

5. **Open your browser**
   Navigate to [http://localhost:3000](http://localhost:3000)

## 🔧 Configuration

### Environment Variables

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `YNAB_ACCESS_TOKEN` | Your YNAB Personal Access Token | ✅ Yes | - |
| `NODE_ENV` | Environment mode | No | `development` |
| `NEXT_PUBLIC_APP_NAME` | Application display name | No | `YNAB Off-Target Analysis` |
| `RATE_LIMIT_REQUESTS_PER_HOUR` | YNAB API rate limit | No | `200` |
| `CACHE_TTL_SECONDS` | Data cache duration | No | `300` |

### Getting Your YNAB Access Token

1. Go to [YNAB Developer Settings](https://app.ynab.com/settings/developer)
2. Click "New Token"
3. Give it a descriptive name (e.g., "Budget Analysis Tool")
4. Copy the generated token
5. Add it to your `.env.local` file

⚠️ **Security Note**: Never commit your actual access token to version control!

## 📊 How to Use

### 1. Select Your Budget
- Choose from your available YNAB budgets
- The most recently modified budget is selected by default

### 2. Choose Analysis Month
- Select any month from your budget's date range
- Navigate between months using the arrow controls

### 3. Review Analysis Results
- **Monthly Overview**: See income, spending, and budget totals
- **Over-Target Categories**: Categories receiving more than their target
- **Under-Target Categories**: Categories receiving less than their target
- **Detailed Category List**: Complete breakdown with variance calculations

### 4. Use Debug Mode (Optional)
- Toggle "Show Debug Information" to see calculation details
- Click debug panels to view:
  - Raw YNAB API fields
  - Applied calculation rules
  - Step-by-step formulas
  - Day counting for weekly goals

## 🧮 Calculation Rules

The application uses a sophisticated 7-rule system to calculate "Needed This Month" values:

1. **Zero-Target Strategy**: Categories without goals → $0
2. **Rule 6**: Future goal creation → $0 (goals created after analysis month)
3. **Rule 1**: Monthly NEED goals → `goal_target`
4. **Rule 2**: Weekly NEED goals → `goal_target × day_occurrences`
5. **Rule 3**: Months to budget → `(goal_overall_left + budgeted) ÷ months_remaining`
6. **Rule 5**: Low months to budget → $0 (completed/overdue goals)
7. **Rule 4**: All other cases → `goal_target`

## 🛠️ Development

### Available Scripts

```bash
npm run dev          # Start development server
npm run build        # Build for production
npm run start        # Start production server
npm run test         # Run test suite
npm run test:watch   # Run tests in watch mode
npm run lint         # Check code quality
npm run type-check   # Verify TypeScript types
```

### Project Structure

```
src/
├── app/                 # Next.js App Router pages
│   ├── api/            # API endpoints
│   └── page.tsx        # Main application page
├── components/         # React components
│   ├── AnalysisDashboard.tsx
│   ├── CategoryDebugPanel.tsx
│   ├── MonthlyOverview.tsx
│   └── ...
├── lib/               # Core business logic
│   ├── data-processing.ts    # Calculation engine
│   ├── monthly-analysis.ts   # Analysis functions
│   └── ynab-service.ts      # YNAB API client
├── types/             # TypeScript interfaces
│   ├── analysis.ts    # Analysis data types
│   └── ynab.ts       # YNAB API types
└── __tests__/         # Test files
```

### Testing

The application includes comprehensive test coverage:

```bash
npm test                    # Run all tests
npm run test:coverage      # Generate coverage report
```

Tests cover:
- All 7 calculation rules
- Edge cases and error handling
- API integration
- Component functionality

## 📚 Documentation

Detailed documentation is available in the `/docs` directory:

- **[Calculation Rules](docs/CALCULATION_RULES.md)** - Complete rule documentation with examples
- **[API Reference](docs/API_REFERENCE.md)** - API endpoints and data structures
- **[Debugging Guide](docs/DEBUGGING_GUIDE.md)** - How to use the debugging UI
- **[Development Guide](docs/DEVELOPMENT_GUIDE.md)** - Technical implementation details

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass (`npm test`)
6. Commit your changes (`git commit -m 'Add amazing feature'`)
7. Push to the branch (`git push origin feature/amazing-feature`)
8. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [YNAB](https://www.ynab.com/) for providing the excellent budgeting platform and API
- [Next.js](https://nextjs.org/) for the amazing React framework
- [Tailwind CSS](https://tailwindcss.com/) for the utility-first CSS framework

## 📞 Support

If you encounter any issues or have questions:

1. Check the [documentation](docs/)
2. Search existing [issues](https://github.com/your-username/YNAB_Off_Target_Assignment/issues)
3. Create a new issue with detailed information

---

**Made with ❤️ for the YNAB community**
