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
        }

    Or even destructure prop objects:

        const Component = ({ wardrobe: { name, colour }}) => {
            console.log(name)
        }