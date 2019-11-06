# AngularBreweries
Use Angular to build a front-end web app.
 
========================================

GOAL: 
Using Angular and NodeJS to build a site: 

========================================

1. Building a SAP with logo and 2 links navigating to 2 pages (Home and Breweries).
    
 ( HOME PAGE )
 
 2. There is a block with a line "You've clicked <this> 1 time.
      - When user clicks in the "this" button, the number following will be incremented.

 3. As a following line, there is a block containing a textbox and a line "You said:" below.
    - When user types any characters or numbers in the textbox, the following line will immediately show out that string of characters or numbers.

  4. Finally, the final block appeared in grey color in the beginning including a line "The click counter is not greater than 4" in the center adjustment.
      - When user clicks the "this" button from 1 to 3 times, this grey block would not change. It will only change to the yellow color if user clicks more than 3 times in that "this" button.
 
( BREWERIES PAGE )

  5. There is a list of companies with 4 items in a line. Each list item describes the company's information in a box such as NAME - location in the top and website address in the bottom.
     
========================================


IMPLEMENTATION

========================================

Step 1: Initializing an Angular Project

========================================
 
 - INSTALL NOTE JS (download and istall)
 
    . Checking NodeJS was intalled or not:
    
       "C:\Users\ProjectName\ node -v"
       
       "C:\Users\ProjectName\ npm -v"
    
 - INSTALL ANGULAR
 
       "C:\Users\ProjectName\ npm i -g @angular/cli"
    
     (ANGULAR CLI - Command Line Interface)
     

 - TEST ANGULAR VERSION:
 
       "C:\Users\ProjectName\ ng version"
   

 - Create a new Project name "my-app"
 
       "C:\Users\ProjectName\ ng new my-app"
   
       "?Would you like to add Angular routing? (y/N) y"
     
       "> SCSS "
   

  - Open the Browser from Command Line AND erecting an NODE JS server
  
        "C:\Users\ProjectName\ ng serve -o"


========================================

Step 2: Modifying Web app

======================================== 

 - Opening the editor app such as Visual Studio Code (installed)
    
       "C:\Users\ProjectName\my-app\ code ."

 - Modifying the file naming "app.component.html"
   . Deleting all lines above <router-outlet></router-outlet>
   . Adding code:
   
       <header>
         <div class="container">
           <a href="#" class="logo">CoolApp</a>
              <nav>
                <ul>
                  <li><a href="#" routerLink="/">Home</a></li>
                  <li><a href="#" routerLink="/list">Breweries</a></li>
                   <!-- using routerLink to connect each page -->
                </ul>
              </nav>
            </div>
         </header> 
 
    . Wrapping the router-outlet line : 
    
         <div class="container">
            <router-outlet></router-outlet>
         </div> 

  - Modifying file : replace all "styles.scss"
    
        @import url('https://fonts.googleapis.com/css?family=Nunito:400,700&display=swap');

        $primary: rgb(111, 0,255); // initializing a variable "primary"

        body{
            margin:0;
            font-family: 'Nunito', sans-serif;
            font-size: 18px;
        }

        .container {
            width: 80%;
            margin: 0 auto;

        }
        header{
            background: $primary;
            padding: 1em 0;

            a{
                color: white;
                text-decoration:  none;
            }

            a.logo{
                font-weight: bold;
            }
            nav {
                float: right;

                ul{
                    list-style-type: none;
                    margin: 0; 

                    display: flex;

                    li a{
                        padding : 1em;
                        &:hover {
                            background: darken($primary, 10%); // increasing darken more 10%
                        }
                    }
                }
            }
            h1{
                margin-top: 2em;
            }
        } 


 - Create 2 components "HOME" and "BREWERIES" for making navigation connecting 2 pages.

      . Open the new cmd window and type to g(generating) and c(creating)
      
          "C:\Users\Project\my-app\ ng g c home"
          "C:\Users\Project\my-app\ ng g c list"

   - Making a connection
      . Opening app-routing.module.ts and Adding more "import":
        
         import { HomeComponent } from './home/home.component';
         import { ListComponent } from './list/list.component';
         

      . Adding more Routing: 
      
         const routes: Routes = [
          {path: '',  component: HomeComponent},
          {path:'list', component: ListComponent }
         ]; 

   - Modifying "home.component.html"
   
         <h1>Welcome!</h1>
         <div class="play-container" >
                     <p>You've clicked <span (click)="countClick()">this</span> {{clickCounter}} times.</p>
         </div>
          <div class="play-container" >
                  <p>
                 <input type="text"  [(ngModel)]="name" > 
          <!--[] means BINDING and () means ON  -->
                        <br/>
                        <strong>You said: </strong> {{name}}
                  </p>
         </div> 

   - Modifying "home.component.scss" 
   
         .play-container{
              border: 1px solid lightgray;
              padding: 3em;
              margin-top: 1em;
              input{
                     padding:1em;
                     margin-bottom:2em;
              }

           }
           span{
              background-color: lightgray;
              font-weight : bold;
              padding : .3em .8em;
              cursor: pointer;
             user-select: none; // quite not familiar 

            }  

    - Modifying "home.component.ts" 
    
          name: string ='hey'; 

    -Modifying "app.module.ts"

         //add more an import line   
         import { FormsModule } from '@angular/forms'; 
         
          // in the square braklet of "imports" as below:
        
          imports: [
            BrowserModule,
            AppRoutingModule, 
          //add more 1 line 
           FormsModule 

    - Using "ngIf" + "ngIfElse" for change status 
    
      . open "home.component.html" and adding as below: 
      
           <div class="play-container" [style.background-color]="clickCounter > 4 ? 'yellow' : 'lightgray'">
               <ng-template [ngIf]="clickCounter > 4" [ngIfElse]="none" )>
                    <p>The click counter is greater than 4</p>
                </ng-template>
                <ng-template #none>
                     <p>The click counter is <strong>NOT greater </strong> than 4</p>
                 </ng-template>
             </div> 

    ****   There are 4 ways to change style here:  ****
    1. Direct in tag line
    
             <div class="play-container" [style.background-color]="clickCounter > 4 ? 'yellow' : 'lightgray'">

    2. Using [ngStyle] 
    
	          <div class="play-container" [ngStyle]="{
                 'background-color'  : clickCounter > 4 ? 'yellow' : 'lightgray',
                 'border'            : clickCounter > 4 ? '4px solid black': 'none'
            }"> 

    3. Using [class.active] 

          <div class="play-container" [class.active]="clickCounter > 4"> 

       . open "home.component.scss" add more style active class 
	
           .active{
               background-color: yellow;
                border: 4px solid black;
           } 


    4. Using [ngClass]
 
	           <div class="play-container" [ngClass]="setClasses()"> 
 
        . open "home.component.ts"  
        
           setClasses(){
               let myClasses ={
                active: clickCounter > 4,
                       notactive : clickCounter <= 4
             }
             return myClasses;
           } 


        . open "home.component.scss" add more style notactive class
 
            .notactive{
                background-color: lightgray;
            } 

    **** END OF 4 ways to change style  *****

  
    
    
    
    
    
