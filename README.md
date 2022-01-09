# react-ts-classcomp-crud

app.tsx

```js
import React, { Component } from 'react';
import { render } from 'react-dom';
import './style.css';

interface AppProps {}

interface AppState {
  employees: IEmployee[];
  employee: IEmployee;
}

interface IEmployee {
  id: number;
  fname: string;
  lname: string;
}

class App extends Component<AppProps, AppState> {
  constructor(props) {
    super(props);

    this.state = {
      employees: [],

      employee: {
        id: -1,
        fname: '',
        lname: '',
      },
    };
  }

  public onRowAdd() {
    this.setState({
      employees: [...this.state.employees, this.state.employee],
    });

    this.setState({
      employee: {
        id: -1,
        fname: '',
        lname: '',
      },
    });
  }

  public onRowEdit(res, index) {
    this.setState({
      employee: {
        id: index,
        fname: res.fname,
        lname: res.lname,
      },
    });
  }

  public onRowUpdate() {
    let employees: any = [...this.state.employees];

    let employee: any = {
      ...employees[this.state.employee.id],
      fname: this.state.employee.fname,
      lname: this.state.employee.lname,
    };

    employees[this.state.employee.id] = employee;

    this.setState({ employees: employees });

    this.setState({
      employee: {
        id: -1,
        fname: '',
        lname: '',
      },
    });
  }

  public onRowDelete(index) {
    this.state.employees.splice(index, 1);

    let employees: any = [...this.state.employees];

    this.setState({ employees: employees });

    this.setState({
      employee: {
        id: -1,
        fname: '',
        lname: '',
      },
    });
  }

  render() {
    return (
      <div>
        <table>
          <tr>
            <th>
              First Name <br />
              <input
                type="text"
                value={this.state.employee.fname}
                onChange={(e: any) => {
                  this.setState({
                    employee: { ...this.state.employee, fname: e.target.value },
                  });
                }}
              ></input>
            </th>

            <th>
              Last Name <br />
              <input
                type="text"
                value={this.state.employee.lname}
                onChange={(e: any) => {
                  this.setState({
                    employee: { ...this.state.employee, lname: e.target.value },
                  });
                }}
              ></input>
            </th>

            <th>
              <div>
                <br />

                {this.state.employee.id >= 0 ? (
                  <div>
                    <input
                      type="button"
                      value="UPDATE"
                      onClick={() => this.onRowUpdate()}
                    />
                  </div>
                ) : (
                  <div>
                    <input
                      type="button"
                      value="ADD"
                      onClick={() => this.onRowAdd()}
                    />
                  </div>
                )}
              </div>
            </th>
          </tr>

          {this.state.employees.map((res, index) => (
            <tr>
              <td style={{ width: '180px' }}>{res.fname}</td>

              <td style={{ width: '180px' }}>{res.lname}</td>

              <td>
                <div>
                  <input
                    type="button"
                    value="Edit"
                    onClick={() => this.onRowEdit(res, index)}
                  />

                  <input
                    type="button"
                    value="Delete"
                    onClick={() => this.onRowDelete(index)}
                  />
                </div>
              </td>
            </tr>
          ))}
        </table>
      </div>
    );
  }
}

render(<App />, document.getElementById('root'));

```
