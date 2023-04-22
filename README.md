1. Explain what the simple List component does :
 
List component is basically a React component that takes a list of items as a props and renders them as a styled list, or customized list, usually with bullet points or numbers for each item, making it easy to identify and naivgate thourgh the items.
It is one of the commonly used react component for web developement for displaying various types of content, such as product lists, blog posts, or navigation menu and navbars.

2. Problems/Warnings in the code : 

Problem 1 : onClick={onClickHandler(index)} the onlick event used here automatically invokes the onclickHandler function everytime the app renders, which is not a good thing.

Solution : We have to modify the code like this:
onClick={onClickHandler(index)} -->> onClick={() => onClickHandler(index)}, so that only when the onlclick event happends the function excutes the onCLickHandler
Here we put the onClickHandler function inside a arrow function so that it invokes the function only when the item is clicked

Problem 2 :
isSelected props value type is set to boolean, but WrappedSingleListItem  is expecting a number.

Solution : We have to modify the code like this :
isSelected: PropTypes.bool -->> isSelected: PropTypes.number
Now instead of boolean we are giving it a number type


Problem 3 : Basically a useState hook syntax goes like this
const [selectedIndex, setSelectedIndex] = useState();
the first value selectedIndex is the currentState
the second value setselectedIndex is the function that is used to update our state.
but in the code the useState is used in a wrong way like this :
const [setSelectedIndex, selectedIndex] = useState();

Solution : 
We have to modify the code like this :
const [setSelectedIndex, selectedIndex] = useState(); -->> const [selectedIndex, setSelectedIndex] = useState();
Now the useState hook's variables are in correct order.

Problem 4 : Wrong dependency in useEffect hook :

Solution : 
We have to modify the code like this :
Wrong code : 
useEffect(() => {
    setSelectedIndex(null);
}, [items]);
  
Corrected Code : 
 useEffect(() => {
    setSelectedIndex(1);
  }, []);
setSelectedIndex(null); -->> setSelectedIndex(1);
so now by default we are giving a true value so the background color will be green
Note : Here value 1 is true and value 0 is false

Problem 5 : 
When mapping with lists each child item in a list should have a unique key to identify each element uniquely.

Solution :
We have to modify the code like this :
Wrong Code :
<ul style={{ textAlign: 'left' }}>
      {items.map((item, index) => (
        <SingleListItem
          onClickHandler={() => handleClick(index)}
          text={item.text}
          index={index}
          isSelected={selectedIndex}/>
  ))}
</ul>
Corrected Code :
<ul style={{ textAlign: 'left' }}>
      {items.map((item, index) => (
        <SingleListItem
          onClickHandler={() => handleClick(index)}
          text={item.text}
          index={index}
          key ={index}
          isSelected={selectedIndex}
        />
      ))}
</ul>

Problem 6 : propTypes.shapeOf is not a valid function instead we should write propTypes.shape() and one more error is we should write arrayOf instead of array

Solution : 
We have to modify the code like this :
Wrong Code :
WrappedListComponent.propTypes = {
  items: PropTypes.array(PropTypes.shapeOf({
    text: PropTypes.string.isRequired,
  })),
};
Corrected Code :
WrappedListComponent.propTypes = {
  items: PropTypes.arrayOf(PropTypes.shape({
    text: PropTypes.string.isRequired,
  })),
};

3. Output of the corrected Code :
![image](https://user-images.githubusercontent.com/76676763/233772824-c1bbbc98-b8fc-4815-adf2-a907048c83d5.png)
