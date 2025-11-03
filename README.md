# rng-life
The most difficult decision made by RNG and interpreted by AI

# 🎰 Random Ideology-Religion-Cheese Slot Machine

A fun, interactive slot machine web application that randomly picks an ideology, religion, and cheese, then uses AI to generate creative commentary about the combination!

## 🎯 Features

- **3 Spinning Slots**: Ideology, Religion, and Cheese categories
- **Realistic Slot Animation**: Smooth spinning effect with staggered stop times
- **AI-Powered Analysis**: Sends combinations to an AI API for creative commentary
- **Fallback Responses**: Built-in humorous messages if API is unavailable
- **Responsive Design**: Works on desktop and mobile devices
- **Visual Effects**: Glowing animations and smooth transitions

## 🚀 How It Works

### The Spinning Mechanism

1. **Click the "SPIN!" button** to start the slot machine
2. Each slot contains 12 different options:
   - **Ideologies**: Capitalism, Socialism, Liberalism, Conservatism, etc.
   - **Religions**: Christianity, Islam, Hinduism, Buddhism, etc.
   - **Cheeses**: Cheddar, Brie, Gouda, Parmesan, etc.

3. **Animation Process**:
   - All three slots start spinning simultaneously
   - Items scroll rapidly through each slot window
   - Slots stop one by one (after 2s, 2.5s, and 3s respectively)
   - Each slot smoothly decelerates to reveal the final selection

### AI Integration

After the slots stop spinning:

1. **Data Collection**: The three selected items are captured
2. **API Request**: Combination is sent to the AI API with a prompt like:
   ```
   "Give me a creative, humorous, and insightful analysis of this 
   random combination: [Ideology] ideology, [Religion] religion, 
   and [Cheese] cheese. Make it entertaining!"
   ```
3. **Response Display**: The AI's commentary appears in a highlighted box below the slots
4. **Fallback Mode**: If the API fails, pre-written humorous messages display instead

## 🛠️ Setup Instructions

### Basic Setup (No AI)

1. Save the HTML file to your computer
2. Open it in any modern web browser
3. Click "SPIN!" to use with fallback messages

### AI API Setup (Full Functionality)

#### Option 1: Using Claude API (Anthropic)

1. Get an API key from [Anthropic Console](https://console.anthropic.com/)
2. In the HTML file, find this line:
   ```javascript
   'x-api-key': 'YOUR_API_KEY_HERE'
   ```
3. Replace `'YOUR_API_KEY_HERE'` with your actual API key
4. Save and reload the page

#### Option 2: Using OpenAI API

Replace the fetch request section with:

```javascript
const response = await fetch('https://api.openai.com/v1/chat/completions', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer YOUR_OPENAI_API_KEY'
    },
    body: JSON.stringify({
        model: 'gpt-4',
        messages: [{
            role: 'user',
            content: `Give me a creative, humorous, and insightful analysis of this random combination in 2-3 sentences: ${ideology} ideology, ${religion} religion, and ${cheese} cheese. Make it entertaining!`
        }],
        max_tokens: 300
    })
});

const data = await response.json();
const analysis = data.choices[0].message.content;
```

#### Option 3: Using Other AI APIs

The code can be adapted for any AI API that accepts text prompts. Just modify:
- The API endpoint URL
- Request headers (authentication)
- Request body format
- Response parsing logic

## 📝 Technical Details

### Technologies Used
- **HTML5**: Structure
- **CSS3**: Styling with gradients, animations, and responsive design
- **Vanilla JavaScript**: Slot animation logic and API integration

### Key Functions

- `createSlotItems()`: Populates each slot with repeated items for smooth scrolling
- `spinSlot()`: Handles individual slot animation with timing and easing
- `spin()`: Orchestrates all three slots and triggers AI analysis
- `analyzeCombo()`: Sends data to AI API and displays results

### Animation Logic

- Each slot's items are duplicated 3 times to create seamless looping
- Linear scrolling during spin phase
- Cubic-bezier easing for smooth deceleration
- Random final position selected from available options

## 🎨 Customization

### Add More Options

Edit the arrays in the JavaScript:

```javascript
const ideologies = ['Your', 'Custom', 'Ideologies', ...];
const religions = ['Your', 'Custom', 'Religions', ...];
const cheeses = ['Your', 'Custom', 'Cheeses', ...];
```

### Change Colors

Modify CSS variables:
- Background gradient: `.body { background: ... }`
- Accent color: `#ffd700` (gold) throughout the CSS
- Slot colors: `.slot { background: ... }`

### Adjust Timing

Change spin duration in the `spin()` function:

```javascript
const durations = [2000, 2500, 3000]; // milliseconds for each slot
```

## ⚠️ Important Notes

### API Rate Limits
- Be mindful of API rate limits and costs
- Each spin makes one API call
- Consider implementing request throttling for public deployments

### Security
- **Never** commit API keys to public repositories
- Use environment variables or server-side proxies for production
- The current implementation exposes API keys in client-side code (for demo only)

### CORS Issues
- API calls may be blocked by CORS policies
- Consider using a backend proxy server for production
- Or use CORS-enabled endpoints if available

## 🐛 Troubleshooting

**Slots not spinning?**
- Check browser console for JavaScript errors
- Ensure all code is properly copied

**AI response not showing?**
- Verify API key is correct
- Check browser console for API errors
- Ensure you have API credits/quota available
- Try the fallback messages first to test basic functionality

**Layout issues on mobile?**
- Clear browser cache
- Try different mobile browsers
- Check responsive CSS media queries

## 📄 License

Free to use and modify for personal and commercial projects.

## 🎉 Have Fun!

Spin away and discover hilarious combinations of ideologies, religions, and cheeses with AI-powered commentary!
