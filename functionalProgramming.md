#####course: https://www.linkedin.com/learning/learning-functional-programming-with-javascript-es6-plus/declarative-vs-imperative-programming?u=200790

##Core concepts of functional programming are:

    1: First class functions:

        https://developer.mozilla.org/en-US/docs/Glossary/First-class_Function

        a function that we can use similar to anything else like numbers or strings such as we can add them etc...

    2: Immutability: 

        When we declare a variable that variable must stay as the initialised value for the entirity of it's life.

        That means that in functional programming instead of updating the value of a variable instead we would create an updated form of that variable:

            const employee = {
                name: 'Joe',
                salary: 2.50
            }

            const updatedEmployee = {
                name: employee.name,
                salary: employee.salary + 1
            }

        Whereas a const can still be changed when working with arrays and objects such as:

        Won't work:

            const numbers = [1, 2, 3, 4, 5];
            numbers = [6, 7, 8 , 9];

            or

            const person = {
                name: 'Joe',
                age: 34
            }
            person = { name: 'Bob' }

        Will work:
        
            const numbers = [1, 2, 3, 4, 5];
            numbers[2] = 4000
            numbers.reverse()

            or

            const person = {
                name: 'Joe',
                age: 34
            }
            person.name = 'Bob'


    3: Seperating functions and data:

        - Object Oriented Programming: functions are along side the data in a class, makes use of {this} keyword

        - Functional Programming: functions are completely seperate from data, makes use of the data being passed as arguments

    4: Pure Functions:

        - nothing inside the function must effect the output

        - no side effects, such as anything that isn't related to calculating the final output


##First class functions:

    one interesting way of using first class functions is to use a functions array:

        const add1 = (x) => x + 1;
        const subtract1 = (x) => x - 1;
        const double = (x) => x * 2;
        const triple = (x) => x * 3;

        const functionsArray = [
            add1,
            subtract1,
            double,
            triple
        ]

        const number 32;

        functionsArray.forEach(func => number = func(number));

        console.log(number);
    
    Another way is to pass functions (anonymous or named) as arguments:

        const reverse = (string) => string.split().reverse().join();
        const upperCase = (string) => string.toUpperCase();

        const performChange = function => function('joseph');

        performChange(reverse);
        performChange(upperCase)
        or
        performChange((string) => string.substring(0,3));

    Returning functions is a smart approach to minimising code (could be useful in testing):

        const createMultiplier = y => x => x * y;

        const double = createMultiplier(2);
        const triple = createMultiplier(3);
        const quadruple = createMultiplier(4);

        double(3)
        triple(7)

    Closures give you access to an outer functions scope from an inner function:

        const createLogger = () => {
            const number = 42;

            return () => console.log(`my number is ${number}`);
        }

        const logger = createLogger();
        logger(); // logs `my number is 42`

        console.log(number) // error

        https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures

    Private variables should only be accessed outside of the scope by calling the functions that return them:

        const Person = ({ name, age, job }) => {
            var _name = name;
            var _age = age;
            var _job = job;

            return {
                getName: () => _name,
                getAge: () => _age,

                setJob: newJob => _job = newJob
            }
        }

        const me = Person({ name: 'Joe', age: 21, job: 'Developer' });
        console.log(me.getName()); // logs `Joe`
        me._name; // would log as undefined

        me.setJob('apprentice developer'); // would log as `apprentice developer`

    Higher Order Functions take functions as arguments or return functions:

        - All functions should each only do one thing (the following example checks for both being zero and dividing)
        - in the following example we don't want our divide function to take in 0 as the second argument:

            Instead of:

                const divide = (x, y) => {
                    if (y === 0) {
                        console.log('error dividing by zero')
                        return null;
                    }

                    return x / y;
                }

                divide(3, 0);
            
            Do this: 

                const divide = (x, y) => x / y;

                const secondArgumentIsntZero = func =>
                    (...arguments) => {
                        if (arguments[1] === 0) {
                            console.log('error dividing by zero')
                            return null;
                        }

                        return func(...arguments)
                    }
            

                const divideSafe = secondArgumentIsntZero(divide);

                console.log(divideSafe(7, 0));

            Another example:

                const words = ['joe', 'dog', 'cat', 'ruubarb', 'donkey'];

                const createLengthTest = minLength =>
                    word => word.length > minLength; // returns this function

                const isLongerThan4 = createLengthTest(4);

                const longWords = words.filter(isLongerThan4) // inside here

        https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments


####A guide to clean code - https://levelup.gitconnected.com/javascript-clean-code-solid-9d135f824180

####Tips: 
- If there is a scenario where you're using defining a new array and and looping over an existing array and pushing into the new array chances are there is a function to help with that e.g map, filter etc
- !! converts an Object to a boolean so that any falsey values will return false such as empty string
- Calling the slice() method on an array with no parameters slice() will copy the whole array and allow you to call other methods after such as array.slice().reverse() in order to avoid mutating the original array e.g
`const clonedArray = array.slice()`
    
        // WILL NOT CLONE
        const array = ['joe', 'poe', 'goe']
        const arrayClone = array;

        arrayClone.push('howard')

        console.log(array) // [ 'joe', 'poe', 'goe', 'howard' ]
        console.log(arrayClone) // [ 'joe', 'poe', 'goe', 'howard' ]

        // WILL CLONE

        const array = ['joe', 'poe', 'goe']
        const arrayClone = array.slice();

        arrayClone.push('howard')

        console.log(array) // [ 'joe', 'poe', 'goe' ]
        console.log(arrayClone) // [ 'joe', 'poe', 'goe', 'howard' ]
- Reduce method takes an array and depending on the function provided makes 1 value out of the array:
        
        const sum = myArray.reduce((acc, element) =>
            acc + element, 0)
        // The 0 is the value that the accumalator should initialise as, this depends on the expected output if returning an array it should start as an empty array
        // The acc is the accumalator which is the sum that the element is being put into eachtime so in this instance the result that each value in the array is being added into.
        // The element is each element in the array

## Advanced Functional Concepts:

    Partial application or Currying is useful when one argument in a function is always the same and simply involves fixing that argument in the function to the set value:

        const add = (x, y, x) => x + y + z;

        // could me turned into:

        const add5 = (x, y) => 5 + y + z;

        // or even better this:

        const add = (x, y, x) => x + y + z;

        const addPartial = x => y => => z => add(x, y, z);

        const add5 = addpartial(6);
        const add5and6 = add5(6);
        const sum = add5and6(7);

        // could be turned into this:

        const add = (x, y, x) => x + y + z;

        const addPartial = x => y => => z => add(x, y, z);

        const sum = addPartial(5)(6)(7)
    

####Things to learn in more detail and try for myself next:
- Higher order functions
- Reduce
