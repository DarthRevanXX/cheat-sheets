
export const ThemeContext = React.createContext()

const [darkTheme, setDarkTheme] = useState(true)

// wrap everything, provided context
```
return (
	<ThemeContext.Provider value = {darlTheme} > </ThemeContext.Provider>
)
```

To access:
```
<ThemeContext.Consumer>
{darkTheme => {
	return <div style={this..themeStyle(darkTheme)}></div>
}}
</ThemeContext.Consumer
```

To access via hook(more simple):
```
const darkTheme = useContext(ThemeContext)
return (
	<div>Function Theme</div>
)
```

Extract to custom theme hook

```
const ThemeContext = React.createContext()
const ThemeUpdateContext = React.createContext()

export function ThemeProvider({childer}) => {
	const [darkTheme, setDarkTheme] = useState(true)

	function toggleTheme() {
		setDarkTheme(prevDarkTheme => !prevDarkTheme)
	}

	const [toggleThemeMemoized, _] = useCallback(() => {toggleTheme})

	return <ThemeContext.Provider value={darkTheme}>
		<ThemeUpdateContext.Provider value = {toggleThemeMemoized}
		{children}
		</ThemeUpdateContext.Provider>
	</ThemeContext.Provider>
}

export function useTheme() {
 return useContext(ThemeContext)
}

export function useThemeUpdate() {
	return useContext(ThemeUpdateContext)
} 
```
