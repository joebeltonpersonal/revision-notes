###React Destructuring
    Rather than:

        const Component = props => {
            console.log(props.wardrobe)
        }

    Or:

        const Component = props => {
            const { wardrobe } = props; 

            console.log(wardrobe)
        }

    you could simplify too:

        const Component = ({ wardrobe }) => {
            console.log(wardrobe)
        })