###Async code
    The foreach loop is a function that calls all of the iterations of the loop at the same time, when faced with a loop that needs to wait for the previous iteration to be completed we can remake the async foreach loop:

        const asyncForEach = async (array, function) => {
            for(i = 0; i < array.length; i++) {
                await functionn(array[i]);
            }
        }

        // for objects:

        await asyncForEach(Object.entries(object), async ([key, value]) => {
            // ...
        })

        // for arrays:

        await asyncForEach(array, async () => {
            // ...
        })