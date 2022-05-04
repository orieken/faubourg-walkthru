Creating the Neighborhood list component
---

## Stories

* Show a list of neighborhood
* Each neighborhood list item has a 'Name', 'Image'

## Missing
* css for the card style


1. In the terminal we can generate our neighborhoods component with `ng g c components/neighborhoods`
2. Now we can add `<app-neighborhoods></app-neighborhoods>` to our `app.component.html`
3. Now we can update our spec to look for the all  in the header:
   From:
   ```typescript
     it('should create', () => {
       expect(component).toBeTruthy();
     });
   ```
   To:
   ```typescript
      it('should show neighborhoods', () => {
        expect(fixture.nativeElement.querySelectorAll('[data-test-id="neighborhood"]').length).toBe(4);
      });
   ```
4. We can add this code in the `neighborhoods.component.html` to make them pass
   ```html
   <div>
     <div data-test-id="neighborhood">Neighborhood 1</div>
     <div data-test-id="neighborhood">Neighborhood 2</div>
     <div data-test-id="neighborhood">Neighborhood 3</div>
     <div data-test-id="neighborhood">Neighborhood 4</div>
   </div>
   ```
5. Now our tests are passing, Ideally we would want to pull this data dynamically from a service. so lets update our code to do that
6. Since we dont have a Service yet we can `Fake it til we make it`
7. lets add a property to our component that will hold the data and we can populate the date in the `ngOnInit` function
   From:
   ```typescript
   import { Component, OnInit } from '@angular/core';
   
   @Component({
     selector: 'app-neighborhoods',
     templateUrl: './neighborhoods.component.html',
     styleUrls: ['./neighborhoods.component.css']
   })
   export class NeighborhoodsComponent implements OnInit {
   
     constructor() { }
   
     ngOnInit(): void {
     }
   }
   ```
   To: 
   ```typescript
   import { Component, OnInit } from '@angular/core';
   import { Observable, of } from 'rxjs';

   @Component({
     selector: 'app-neighborhoods',
     templateUrl: './neighborhoods.component.html',
     styleUrls: ['./neighborhoods.component.css']
   })
   export class NeighborhoodsComponent implements OnInit {
     neighborhoods$!: Observable<any>;

     constructor() { }

     ngOnInit(): void {
       this.neighborhoods$ = of([
       {
         name: 'Marigny',
         image: 'assets/marigny.jpg',
       },
       {
         name: 'Vieux Carre',
         image: 'assets/vieux-carre.jpg',
       },
       {
         name: 'Freret',
         image: 'assets/freret.jpg',
       },
       {
         name: 'Carrollton',
         image: 'assets/carrollton.jpg',
        },
      ])
    }
   }
   ```
8. Now we can update our `neighborhoods.component.html` to iterate over the `neighborhoods$` Observable
   To: 
   ```html
   <div>
     <div data-test-id="neighborhood" *ngFor="let neighborhood of neighborhoods$ | async" >Neighborhood</div>
   </div>
   ```
   And, our specs should still be passing
9. We can use the data from our observable to put the name and image in our neighborhood div, so lets write a test for it
   ```typescript
   it('should show neighborhood information', () => {
     const neighborhood = fixture.nativeElement.querySelector('[data-test-id="neighborhood"]');
     expect(neighborhood.querySelector('[data-test-id="name"]').innerText).toEqual('Marigny');
   });
   ```
10. With our failing test we can update our `neighborhoods.component.html` 
    To:
    ```html
    <div>
        <div data-test-id="neighborhood" *ngFor="let neighborhood of neighborhoods$ | async" >
            <div data-test-id="name">{{ neighborhood.name }}</div>
        </div>
    </div>
    ```
11. And our test is passing again.
12. Now lets update the test to look for the neighborhood image
    ```typescript
    it('should show neighborhood information', () => {
      const neighborhood = fixture.nativeElement.querySelector('[data-test-id="neighborhood"]');
      expect(neighborhood.querySelector('[data-test-id="name"]').innerText).toEqual('Marigny');
      expect(neighborhood.querySelector('[data-test-id="image"]').src).toContain('assets/marigny.jpg')
    });
    ```
13. And to make it pass by adding the image tag
    To:
   ```html
   <div>
       <div data-test-id="neighborhood" *ngFor="let neighborhood of neighborhoods$ | async" >
           <div data-test-id="name">{{ neighborhood.name }}</div>
           <div data-test-id="image"><img src="{{ neighborhood.image }}" /></div>
       </div>
   </div>
   ```
