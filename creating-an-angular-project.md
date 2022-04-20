Creating an Angular Project
___

## Installing
1. Install brew `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
2. Install NVM `brew install nvm`
3. Install Node 16 `nvm install 16`
4. Install Angular `npm install -g @angular/cli`
5. Make a Projects dir in your home dir `cd ~ && mkdir Projects && cd Projects`
6. Create a new project with angular cli `ng new faubourg` // its pronounced FO-burg
   1. Would you like to add Angular routing? `No`
   2. Which stylesheet format would you like to use? `CSS`
7. Change directory to our new angular project `cd faubourg` 
   1. Cleanup and get project ready for TDD
      1. open the project in the editor of your choice. 
         1. For Webstorm use `webstorm .` (I will be using Webstorm)
         2. For VSCode use `code .`
      2. Delete all of the contents of `app.component.html`
      3. Change `app.component.spec.ts` 
       From:
      ```typescript
      import { TestBed } from '@angular/core/testing';
      import { AppComponent } from './app.component';
   
      describe('AppComponent', () => {
        beforeEach(async () => {
          await TestBed.configureTestingModule({
            declarations: [
              AppComponent
            ],
          }).compileComponents();
        });
   
        it('should create the app', () => {
          const fixture = TestBed.createComponent(AppComponent);
          const app = fixture.componentInstance;
          expect(app).toBeTruthy();
        });
   
        it(`should have as title 'faubourg'`, () => {
          const fixture = TestBed.createComponent(AppComponent);
          const app = fixture.componentInstance;
          expect(app.title).toEqual('faubourg');
        });
   
        it('should render title', () => {
          const fixture = TestBed.createComponent(AppComponent);
          fixture.detectChanges();
          const compiled = fixture.nativeElement as HTMLElement;
          expect(compiled.querySelector('.content span')?.textContent).toContain('faubourg app is running!');
        });
      });
      ``` 
      To: 
      ```typescript
      describe('AppComponent', () => {
        it('this spec is true because empty specs are deprecated', () => {
          expect(true).toBeTruthy();
        });
      });
      ```
8. Now we can open 3 terminals in this dir `Command key + t`
   1. Terminal 1 we will run `npm test` this lets us know the tests are working with our one spec
   2. Terminal 2 we will run `npm start` this lets us know that the app works  
   3. Terminal 3 will be for adding any other packages we may need along the way.
9. We can open a browser to `http://localhost:4200/` and should see a blank html page

## Next up
[Header Component](./header-component.md)
