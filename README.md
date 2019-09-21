# Hyperledger-study-15

하이퍼레져 앱 만들기 실습 15일차 - 이벤트를 활용하여 버튼 클릭시 내용 변경되는 기능 구현

출처 : https://www.opentutorials.org/module/4058/24737

1. 14일차 예제 앱 사용

2. App.js에 state 추가

        constructor(props){
            super(props);
            this.state = {
              mode:"read",
              subject:{title:"WEB", sub:"World Wide Web!"},
              welcome:{title:"Welcome", desc:"Hello, React!!"},
              contents:[
                {id:1, title:"HTML", desc:"HTML is for information"},
                {id:2, title:"CSS", desc:"CSS is for design"},
                {id:3, title:"JavaScript", desc:"JavaScript is for interactive"}
              ]
            }
          }
 
 3. render에 if문 추가
 
         render() {
            console.log('App render');
            var _title, _desc = null;
            if(this.state.mode === 'welcome'){
              _title = this.state.welcome.title;
              _desc = this.state.welcome.desc;
            } else if(this.state.mode === 'read'){
              _title = this.state.contents[0].title;
              _desc = this.state.contents[0].desc;
            }
         }

4. return에 bind와 setState 사용

        return (
              <div className="App">
               {/* <Subject 
               title={this.state.subject.title} 
               sub={this.state.subject.sub}>
               </Subject> */}
                <header>
                  <h1><a href="/" onClick={function(e){
                    console.log(e);
                    e.preventDefault();
                    //this.state.mode = 'welcome';
                    this.setState({
                      mode:"welcome"
                    })
                  }.bind(this)}>{this.state.subject.title}</a></h1>
                  {this.state.subject.sub}
                </header>
               <Nav data={this.state.contents}></Nav>
               <ART title={_title} desc={_desc}></ART>
              </div>
            );

5. 최종 App.js 코드

        import React, {Component} from 'react';
        import './App.css';
        import Nav from "./components/Nav"
        import Subject from "./components/Subject"
        import ART from "./components/ART"

        class App extends Component {
          //초기화 담당
          constructor(props){
            super(props);
            this.state = {
              mode:"read",
              subject:{title:"WEB", sub:"World Wide Web!"},
              welcome:{title:"Welcome", desc:"Hello, React!!"},
              contents:[
                {id:1, title:"HTML", desc:"HTML is for information"},
                {id:2, title:"CSS", desc:"CSS is for design"},
                {id:3, title:"JavaScript", desc:"JavaScript is for interactive"}
              ]
            }
          }

          render() {
            console.log('App render');
            var _title, _desc = null;
            if(this.state.mode === 'welcome'){
              _title = this.state.welcome.title;
              _desc = this.state.welcome.desc;
            } else if(this.state.mode === 'read'){
              _title = this.state.contents[0].title;
              _desc = this.state.contents[0].desc;
            }
            return (
              <div className="App">
               {/* <Subject 
               title={this.state.subject.title} 
               sub={this.state.subject.sub}>
               </Subject> */}
                <header>
                  <h1><a href="/" onClick={function(e){
                    console.log(e);
                    e.preventDefault();
                    //this.state.mode = 'welcome';
                    this.setState({
                      mode:"welcome"
                    })
                  }.bind(this)}>{this.state.subject.title}</a></h1>
                  {this.state.subject.sub}
                </header>
               <Nav data={this.state.contents}></Nav>
               <ART title={_title} desc={_desc}></ART>
              </div>
            );
          }  
        }

        export default App;

6. 'WEB'을 누르면 mode가 read에서 welcome으로 변경되면서 ART의 내용도 변경된다.

