Creating a Header component
---

## Stories

* header has the app name
* header has a logo
* header has navigation items 'Places', 'Map', 'Add'

## Missing

* logo image
* css styling

1. Lets start off by generating our component with `ng g c components/header`
2. Now we can add `<app-header></app-header>` to our `app.component.html`
3. Now we can update our spec to look for the App name in the header:  
   From:
    ```typescript
    it('should create', () => {
      expect(component).toBeTruthy();
    });
    ```
   To:
    ```typescript
    it('should show app name', () => {
      expect(fixture.nativeElement.querySelector('[data-test-id="app-name"]')).toBeTruthy()
    });
    ```
4. Next we add the simplest code in our `header.component.html` to make the spec pass:
   ```html
   <header>
    <h2 data-test-id="app-name">faubourg</h2>
   </header>
   ``` 
5. We can move on to adding the test for the logo:
   ```typescript
   it('should show the Logo', () => {
    expect(fixture.nativeElement.querySelector('[data-test-id="logo"]')).toBeTruthy()
   });
   ```
6. Another failing spec now we can add the code `header.component.html` to make it pass:
   ```html
    <a href="/" title="Return to the homepage" data-test-id="logo" id="logo">
        <img src="favicon.ico" width="40" alt="Faubourg logo" />
    </a>
   ```
7. Now we can add a final spec for the nav items:
   ```typescript
     it('should show menu', () => {
       expect(fixture.nativeElement.querySelector('[data-test-id="menu"]')).toBeTruthy();
     });
   ```
8. Adding the nav block should be enough to make the spec pass:
   ```html
   <nav data-test-id="menu"></nav>
   ```
9. And finally a spec for the menu-items:
   ```typescript
     it('should show menu items', () => {
       expect(fixture.nativeElement.querySelector('[data-test-id="places"]')).toBeTruthy();
       expect(fixture.nativeElement.querySelector('[data-test-id="map"]')).toBeTruthy();
       expect(fixture.nativeElement.querySelector('[data-test-id="add-place"]')).toBeTruthy();
     });
   ```
10. Now lets make it pass with:
   ```html
     <ul>
       <li data-test-id="places"><a href="/places" title="View all places">Places</a></li>
       <li data-test-id="map"><a href="/map" title="View map of places">Map</a></li>
       <li data-test-id="add-place"><a href="/add-place" title="Add a new place">Add a place</a></li>
     </ul>
   ```
