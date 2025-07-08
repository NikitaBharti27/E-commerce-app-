# E-commerce-app-
 React Concepts Applied: E-Commerce App Scenario
You have a ProductCard component that displays a product’s name and price.
Q1: How will you pass these values from the parent component?
Ans: By using props. The parent component will pass name and price like this:
<ProductCard name="iPhone" price={9000} />
And ProductCard will receive them like:
const ProductCard = ({ name, price }) => (
  <div>
    <h2>{name}</h2>
    <p>₹{price}</p>
  </div>
);

Each product has a "Like" button that toggles between "Liked ❤️" and "Like 🤍".
Q2: How will you implement this toggle using useState?
Ans:I'll use a boolean state to track whether the product is liked. When the button is clicked, the state toggles between true and false.
const [liked, setLiked] = useState(false);
<button onClick={() => setLiked(!liked)}>
  {liked ? "Liked ❤️" : "Like 🤍"}
</button>

There’s a search input at the top to filter products as the user types.
Q3: How will you manage this input using a controlled component approach?
Ans:I'll use a boolean state to track whether the product is liked. When the button is clicked, the state toggles between true and false.
const [liked, setLiked] = useState(false);
<button onClick={() => setLiked(!liked)}>
  {liked ? "Liked ❤️" : "Like 🤍"}
</button>

Your app supports light and dark themes.
Q4: How will you share the current theme across all components using useContext?
Ans:I’ll create a ThemeContext using React’s Context API. The theme (light/dark) is stored in a context provider at the top level, and any child component can access it using useContext.
// ThemeContext.js
export const ThemeContext = createContext();
export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState("light");

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};
// In any component
const { theme } = useContext(ThemeContext);
This avoids prop-drilling and keeps the theme logic centralized.

The "Checkout" page should only be accessible to logged-in users.
Q5: How will you protect this route to restrict unauthenticated access?
Ans:I’ll check if the user is authenticated before allowing access to the checkout page. If they’re not logged in, I’ll redirect them to the login page.
const PrivateRoute = ({ children }) => {
  const isAuthenticated = useAuth(); // your custom auth logic

  return isAuthenticated ? children : <Navigate to="/login" />;
};
And in the routes:
<Route
  path="/checkout"
  element={
    <PrivateRoute>
      <CheckoutPage />
    </PrivateRoute>
  }
/>
This makes sure only logged-in users can proceed to checkout, just like you'd expect in a real store.
