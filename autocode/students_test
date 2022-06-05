package coverage

import (
	"os"
	"testing"
	"time"
	"errors"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func TestPeopleLen_Nil(t *testing.T){
	var p People
	var expectedLen int = 0
	var len int = p.Len()
	if (len != expectedLen){
		t.Errorf("Expected: %d, got %d", expectedLen, len)
	}
}

func TestPeopleLen_Capacity(t *testing.T){
	var p People = make(People,0,10)
	var expectedLen int = 0
	var len int = p.Len()
	if (len != expectedLen){
		t.Errorf("Expected: %d, got %d", expectedLen, len)
	}
}

func TestPeopleLen_Len(t *testing.T){
	var expectedLen int = 10
	var p People = make(People,expectedLen)	
	var len int = p.Len()
	if (len != expectedLen){
		t.Errorf("Expected: %d, got %d", expectedLen, len)
	}
}

func TestPeopleLess(t *testing.T) {
	dF, err := time.Parse(time.RFC3339, "2000-03-05T00:00:00Z")
	if (err != nil){
		t.Errorf("time.Parse error %s", err)
	}

	dS, err := time.Parse(time.RFC3339, "2000-03-06T00:00:00Z")
	if (err != nil){
		t.Errorf("time.Parse error %s", err)
	}

	tData := []struct {
		F Person
		S Person
		Expected bool
		Inverted bool
	}{
		{F: Person{firstName:"Александр",lastName:"Иванов",birthDay: dF}, S: Person{firstName:"Александр",lastName:"Иванов",birthDay: dF}, Expected: false, Inverted: false},
		{F: Person{firstName:"Александр",lastName:"Иванов",birthDay: dF}, S: Person{firstName:"Александр",lastName:"Иванов",birthDay: dS}, Expected: false, Inverted: true}, //true, false
		{F: Person{firstName:"Александр",lastName:"Иванов",birthDay: dF}, S: Person{firstName:"Александр",lastName:"Сидоров",birthDay: dF}, Expected: true, Inverted: false},
		{F: Person{firstName:"Александр",lastName:"Иванов",birthDay: dF}, S: Person{firstName:"Александр",lastName:"Сидоров",birthDay: dS}, Expected: false, Inverted: true},//true, false
		{F: Person{firstName:"Александр",lastName:"Иванов",birthDay: dF}, S: Person{firstName:"Владимир",lastName:"Иванов",birthDay: dF}, Expected: true, Inverted: false},
		{F: Person{firstName:"Александр",lastName:"Иванов",birthDay: dF}, S: Person{firstName:"Владимир",lastName:"Иванов",birthDay: dS}, Expected: false, Inverted: true},//true, false
		{F: Person{firstName:"Александр",lastName:"Иванов",birthDay: dF}, S: Person{firstName:"Владимир",lastName:"Сидоров",birthDay: dF}, Expected: true, Inverted: false},
		{F: Person{firstName:"Александр",lastName:"Иванов",birthDay: dF}, S: Person{firstName:"Владимир",lastName:"Сидоров",birthDay: dS}, Expected: false, Inverted: true},//true, false
	}

	for i, v := range tData {
		p := make(People, 2)
		p[0] = v.F;
		p[1] = v.S;
		got := p.Less(0, 1)
		if got != v.Expected {
			t.Errorf("Expected: %t, got %t. Index = %d, first = %v, second = %v", v.Expected, got, i, v.F, v.S)
		}

		got = p.Less(1, 0)
		if got != v.Inverted {
			t.Errorf("Expected: %t, got %t. Inverted.Index = %d, first = %v, second = %v", v.Inverted, got, i, v.F, v.S)
		}
	}
}

func TestPeopleSwap(t *testing.T) {
	dF, err := time.Parse(time.RFC3339, "2000-03-05T00:00:00Z")
	if (err != nil){
		t.Errorf("time.Parse error %s", err)
	}

	dS, err := time.Parse(time.RFC3339, "2000-03-06T00:00:00Z")
	if (err != nil){
		t.Errorf("time.Parse error %s", err)
	}
	F := Person{firstName:"Александр",lastName:"Иванов",birthDay: dF}
	S := Person{firstName:"Владимир",lastName:"Сидоров",birthDay: dS}
	p := make(People, 5)
	p[2] = F
	p[4] = S
	p.Swap(2, 4)
	if p[2] != S {
		t.Errorf("Expected: %v, got %v", S, p[2])
	} else if p[4] != F {
		t.Errorf("Expected: %v, got %v", F, p[4])
	}
}

func CompareIntSlice(f, s []int) bool{
	if len(f) != len(s){
		return false
	}
	for i := 0; i < len(f); i++ {
		if f[i] != s[i]{
			return false
		}
	}
	return true
}

func CompareMaxtrix(f, s Matrix) bool{
	return f.rows == s.rows && f.cols == s.cols && CompareIntSlice(f.data, s.data)
}

func TestMatrixNew(t *testing.T) {
	tData := []struct {
		S string
		Expected Matrix
		Err error
	}{
		{S: "", Expected: Matrix{rows: 0,cols: 0, data: nil}, Err: errors.New("strconv.Atoi: parsing \"\": invalid syntax")},
		{S: "1", Expected: Matrix{rows: 1,cols: 1, data: []int{1}}, Err: nil},
		{S: "A", Expected: Matrix{rows: 0,cols: 0, data: nil}, Err: errors.New("strconv.Atoi: parsing \"A\": invalid syntax")},
		{S: "\n", Expected: Matrix{rows: 0,cols: 0, data: nil}, Err: errors.New("strconv.Atoi: parsing \"\": invalid syntax")},		
		{S: "1\n", Expected: Matrix{rows: 0,cols: 0, data: nil}, Err: errors.New("strconv.Atoi: parsing \"\": invalid syntax")},
		{S: "1\n2 3", Expected: Matrix{rows: 0,cols: 0, data: nil}, Err: errors.New("Rows need to be the same length")},
		{S: "1 2\n2", Expected: Matrix{rows: 0,cols: 0, data: nil}, Err: errors.New("Rows need to be the same length")},
		{S: "11 22\n33 44\n55 66", Expected: Matrix{rows: 3,cols: 2, data: []int{11, 22, 33, 44, 55, 66}}, Err: nil},
	}
	
	for i, v := range tData {
		m, err := New(v.S)
		if err != nil || v.Err != nil {
			var errAsString string
			var vErrAsString string
			if err != nil {
				errAsString = err.Error()
			}
			if v.Err != nil {
				vErrAsString = v.Err.Error()
			}
			if errAsString != vErrAsString{
				t.Errorf("Expected error: %s, got %s. Index = %d", v.Err, err, i)
			}
		} else {
			_m := *m
			if !CompareMaxtrix(_m, v.Expected) {			
				t.Errorf("Expected: %v, got %v. Index = %d", v.Expected, _m, i)
			}
		}
	}
}

func CompareTwoDimIntSlice(f, s [][]int) bool{
	if len(f) != len(s){
		return false
	}
	for i := 0; i < len(f); i++ {
		if !CompareIntSlice(f[i], s[i]){
			return false
		}
	}
	return true
}

func TestMatrixRows(t *testing.T) {
	tData := []struct {
		M Matrix
		Expected [][]int
	}{
		{M: Matrix{rows: 0,cols: 0, data: nil}, Expected: nil},
		{M: Matrix{rows: 1,cols: 1, data: []int{1}}, Expected: [][]int{{1}}},
		{M: Matrix{rows: 3,cols: 2, data: []int{11, 22, 33, 44, 55, 66}}, Expected: [][]int{{11,22},{33,44},{55,66}}},
	}
	
	for i, v := range tData {
		r := v.M.Rows()
		if !CompareTwoDimIntSlice(r, v.Expected) {			
			t.Errorf("Expected: %v, got %v. Index = %d", v.Expected, r, i)
		}
	}
}

func TestMatrixCols(t *testing.T) {
	tData := []struct {
		M Matrix
		Expected [][]int
	}{
		{M: Matrix{rows: 0,cols: 0, data: nil}, Expected: nil},
		{M: Matrix{rows: 1,cols: 1, data: []int{1}}, Expected: [][]int{{1}}},
		{M: Matrix{rows: 3,cols: 2, data: []int{11, 22, 33, 44, 55, 66}}, Expected: [][]int{{11,33,55},{22,44,66}}},
	}
	
	for i, v := range tData {
		r := v.M.Cols()
		if !CompareTwoDimIntSlice(r, v.Expected) {			
			t.Errorf("Expected: %v, got %v. Index = %d", v.Expected, r, i)
		}
	}
}

func TestMatrixSet(t *testing.T) {
	tData := []struct {
		M Matrix
		Row, Col, Value int
		Expected bool
	}{
		{M: Matrix{rows: 0,cols: 0, data: nil}, Row:0, Col:0, Value:0, Expected: false},
		{M: Matrix{rows: 0,cols: 0, data: nil}, Row:1, Col:0, Value:0, Expected: false},
		{M: Matrix{rows: 0,cols: 0, data: nil}, Row:0, Col:1, Value:0, Expected: false},
		{M: Matrix{rows: 1,cols: 1, data: []int{1}}, Row:0, Col:0, Value:1, Expected: true},
		{M: Matrix{rows: 1,cols: 1, data: []int{1}}, Row:0, Col:0, Value:2, Expected: true},
		{M: Matrix{rows: 3,cols: 2, data: []int{11, 22, 33, 44, 55, 66}}, Row:-1, Col:-1, Value:77, Expected: false},
		{M: Matrix{rows: 3,cols: 2, data: []int{11, 22, 33, 44, 55, 66}}, Row:-1, Col:1, Value:77, Expected: false},
		{M: Matrix{rows: 3,cols: 2, data: []int{11, 22, 33, 44, 55, 66}}, Row:1, Col:-1, Value:77, Expected: false},
		{M: Matrix{rows: 3,cols: 2, data: []int{11, 22, 33, 44, 55, 66}}, Row:1, Col:1, Value:77, Expected: true},
		{M: Matrix{rows: 2,cols: 3, data: []int{11, 22, 33, 44, 55, 66}}, Row:1, Col:1, Value:77, Expected: true},
	}
	
	for i, v := range tData {
		m := &(v.M)
		r := m.Set(v.Row, v.Col, v.Value)
		if r != v.Expected {
			t.Errorf("Expected: %t, got %t. Index = %d, M = %v", v.Expected, r, i, m)
		} else if r && m.data[v.Row*m.cols+v.Col] != v.Value {			
			t.Errorf("Expected: %d, got %d. Index = %d, Row = %d, Col = %d, M = %v", v.Value, m.data[v.Row+v.Col], i, v.Row, v.Col, m)
		}
	}
}