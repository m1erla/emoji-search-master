# Emoji Test Img


![ss](public/assets/emoji-tests.png)


---

# Code Blocks

```

import {render, screen, fireEvent, waitFor } from "@testing-library/react";
import '@testing-library/jest-dom';
import emojiList from "../emojiList.json";
import App from "../App";

describe("Emoji input tests", () => {
    let header, input, filterList, emoji;

    beforeEach(() => {
        render(<App/>);
    });

    it("Header is rendered successfully tests", async() => {
        header = screen.getByText(/Emoji Search/i);

        await waitFor(() => {

            expect(header).toBeInTheDocument();
            const images = screen.getAllByRole("img");
            expect(images[0]);
            expect(images[1]);

        });
    });

        test("Emoji list is rendered successfully first opened tests", () => {
          
              emoji = emojiList.slice(0, 19);

              emoji.map((item) => {expect(screen.getByText(item.title)).toBeInTheDocument()});
           
        });

        test("Emoji list is re-rendered according to that filter tests", () => {

            input = screen.getByRole("textbox");
            const filter = "smile cat";

            filterList = emojiList.filter(
                it => 
                it.keywords.toLowerCase().match(filter) || 
                it.title.toLowerCase().match(filter))

            fireEvent.change(input, {target: {value: filter}});

            expect(screen.getAllByText(/cat/i)).toHaveLength(2);

        });


       test("Check that the relevant emoji is copied. tests", async() => {
        
        await waitFor(() => {
            const click = screen.getByText("Heart Eyes");
            expect(click.parentElement.getAttribute("data-clipboard-text").length).toBeGreaterThan(0);
            console.log(click.parentElement.getAttribute("data-clipboard-text"));
            expect(click.parentElement.getAttribute("data-clipboard-text")).toMatch("😍");

        });
       });
       
   
})


```

---

Created with *create-react-app*. See the [full create-react-app guide](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md).



Install

First you have to install yarn, then you should also install dependencies and some upgrades from below.
---
`yarn add react-scripts`

`yarn upgrade @testing-library/react@release-12.x`

`yarn add --dev @testing-library/jest-dom`

`yarn add --dev @testing-library/user-event`

`yarn add  @testing-library/dom`
  

`npm install`



Usage
---
`yarn start`

`npm start`

`yarn test`

`npm test`
