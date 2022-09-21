package awesomeProject

import "fmt"

type Subject interface {
	RegisterObserver(o Observer)
	RemoveObserver(o Observer)
	NotifyObserver()
}
type ScoreUpdater struct {
	score        int
	observerList []Observer
}

type Observer interface {
	Update(value int)
}

type User struct {
	name          string
	score         int
	simpleSubject Subject
}

func NewUser(ss Subject, name string) *User {
	newUser := &User{
		name:          name,
		simpleSubject: ss,
	}
	newUser.simpleSubject.RegisterObserver(newUser)
	return newUser
}

func (u *User) Update(score int) {
	u.score = score
	u.display()

}
func (u *User) display() {
	fmt.Printf("%s received score updates:%d\n", u.name, u.score)
}
func NewScoreUpdater() *ScoreUpdater {
	return &ScoreUpdater{
		score:        0,
		observerList: make([]Observer, 0),
	}
}
func (su *ScoreUpdater) RegisterObserver(o Observer) {
	su.observerList = append(su.observerList, o)
}
func (su *ScoreUpdater) RemoveObserver(o Observer) {
	found := false
	i := 0
	for ; i < len(su.observerList); i++ {
		if su.observerList[i] == o {
			found = true
			break
		}
	}
	if found {
		su.observerList = append(su.observerList[:i], su.observerList[i+1:]...)
	}
}

func (su *ScoreUpdater) NotifyObserver() {
	for _, observer := range su.observerList {
		observer.Update(su.score)
	}
}

func (su *ScoreUpdater) SetValue(value int) {
	su.score = value
	su.NotifyObserver()
}
func main() {
	simpleSubject := NewScoreUpdater()
	NewUser(simpleSubject, "Bob")
	NewUser(simpleSubject, "Thomas")
	NewUser(simpleSubject, "Carl")
	c := NewUser(simpleSubject, "Robert")
	simpleSubject.SetValue(50)
	simpleSubject.RemoveObserver(c)
	simpleSubject.SetValue(60)
}
