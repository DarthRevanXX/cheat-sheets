This is because of StrictMode. It new double renders useEffects on the first render since StrictMode double mounts components on initial mount

const handleResize = () => {
	setWindowSize(window.innerWidth)
}
Clean up 
useEffect (()=> {
	window.addEventListener('resize', handleResize)

	return () => {
		window.removeEventListener('resize', handleResize)
	}
})

return run first