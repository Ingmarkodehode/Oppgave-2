`const formEL= document.getElementById("build-order")` setter formEl til elementet med id buildorder

`const buildText = document.getElementById("txtbox")` setter buildText til elementet med id txtbox

`const buildContainer = document.getElementById("build")` setter buildContainer til elementet med id build

`const localStorageKey = "buildlist"` setter localstoragekey til buildlist

`const deleteBuild = document.getElementById("build-delete")` setter deleteBuild til elementet med id build-delete

`let buildlist = JSON.parse(localStorage.getItem(localStorageKey)) || []` setter buildlist til og inneholde det samme som localstorage. Om localstorage er tom settes buildlist til ett tomt array

`buildlist.forEach((buildItem) => createBuildHtml(buildItem.name, buildItem.id));`

`function addBuild(text) {`
`const buildId = Date.now()`
`buildlist.push({`
`name: text,`
`id: buildId`
`localStorage.setItem(localStorageKey, JSON.stringify(buildlist))`
`createBuildHtml(text, buildId)`

`function createBuildHtml(text, buildId) {`

`const container = document.createElement("div")`
`container.style = "display: flex;"`

`const paragraph = document.createElement("p")`
`paragraph.textContent = text`

`const button = document.createElement("button")`
`button.textContent = "Remove todo"`

`button.addEventListener("click", () => removeTodo(container, buildId))`

`container.append(paragraph, button)`
`buildContainer.appendChild(container)`

`function removeTodo(element, buildId) {`
`buildlist = buildlist.filter((build) => build.id !== buildId) `
`localStorage.setItem(localStorageKey, JSON.stringify(buildlist))`
`element.remove()`
`deleteBuild.addEventListener("click", function() {`
`localStorage.clear();`
`buildlist = [];`
`while (buildContainer.firstChild) {`
`buildContainer.firstChild.remove()`
`function handleBuild(event){`
`event.preventDefault()`
`if (buildText.value.length < 3) return`
`addBuild(buildText.value)`
`buildText.value = ""`
`formEL.addEventListener("submit", handleBuild)`

# full code

const formEL= document.getElementById("build-order") //setter formEL til build-order
const buildText = document.getElementById("txtbox") //setter textInput til txtbox
const buildContainer = document.getElementById("build") //setter build til build
const localStorageKey = "buildlist" //setter localstoragekey til buildlist1
const deleteBuild = document.getElementById("build-delete")
let buildlist = JSON.parse(localStorage.getItem(localStorageKey)) || []

buildlist.forEach((buildItem) => createBuildHtml(buildItem.name, buildItem.id));

function addBuild(text) {
const buildId = Date.now()
buildlist.push({
name: text,
id: buildId
})
localStorage.setItem(localStorageKey, JSON.stringify(buildlist))
createBuildHtml(text, buildId)
}

function createBuildHtml(text, buildId) {

    const container = document.createElement("div")
    container.style = "display: flex;"

    const paragraph = document.createElement("p")
    paragraph.textContent = text

    const button = document.createElement("button")
    button.textContent = "Remove todo"

    // add event listener to the remove todo button
    button.addEventListener("click", () => removeTodo(container, buildId))

    container.append(paragraph, button)
    buildContainer.appendChild(container)

}

function removeTodo(element, buildId) {
buildlist = buildlist.filter((build) => build.id !== buildId)
localStorage.setItem(localStorageKey, JSON.stringify(buildlist))

    element.remove()

}

deleteBuild.addEventListener("click", function() {
localStorage.clear();
buildlist = [];

    while (buildContainer.firstChild) {
        buildContainer.firstChild.remove()
    }

})

function handleBuild(event){
event.preventDefault()
if (buildText.value.length < 3) return

    addBuild(buildText.value)
    buildText.value = ""

}

formEL.addEventListener("submit", handleBuild)
