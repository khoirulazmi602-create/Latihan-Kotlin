//data class Product (val name : String, val price : Int)
    
//fun Product.isPassed() : Boolean = price >= 7000

//fun main() {
    //val  nasi = Product("nasi", 8000) 
    //val nasiBaru = nasi.copy(price = 17000)
    
    
    //println(nasi)
    //println("Apakah nasi kebuli mahal" + nasiBaru.isPassed())// true
    
//}

//fun main(){
    
//val cart = mutableListOf("Laptop", "Mouse")
    //cart.add("Keyboard")
    //cart.add("Headset")
    //cart.remove("Mouse")
    
    //println(cart)
    
    //for (n in cart){
        //println(n)
    //}
    
    //println(cart. size)
//}




enum class CourseStatus {
    ACTIVE,
    COMPLETED
}

data class Course(
    val code: String,
    val name: String,
    val status: CourseStatus
) {
    companion object {
        const val PREFIX = "PAB"
    }
}

fun Course.displayInfo(): String {
    return "$code - $name - $status"
}



fun describe(status: CourseStatus): String {
    return when (status) {
        CourseStatus.ACTIVE -> "Mata kuliah sedang aktif"
        CourseStatus.COMPLETED -> "Mata kuliah sudah selesai"
    }
}



object AppConfig {
    const val MAX_COURSES = 5
}

fun MutableList<Course>.addCourse(course: Course): Boolean {
    if (size >= AppConfig.MAX_COURSES) {
        return false
    }

    if (!course.code.startsWith(Course.PREFIX)) {
        return false
    }

    add(course)
    return true
}



fun main() {

    val courses = mutableListOf(
        Course("PAB101", "B.ARAB", CourseStatus.ACTIVE),
        Course("PAB102", "SCPK", CourseStatus.COMPLETED),
        Course("PAB103", "PAIM", CourseStatus.ACTIVE)
    )

  
    courses.add(
        Course("PAB104", "BIG DATA", CourseStatus.ACTIVE)
    )

    
    courses.removeAt(1)


    println("=== DAFTAR MATA KULIAH ===")

    for (course in courses) {
        println(course.displayInfo())
    }


    
    val course = courses[0]

    val (code, name, status) = course

    println("=== DESTRUCTURING ===")
    println("Code   : $code")
    println("Name   : $name")
    println("Status : $status")


    
    println("=== DESKRIPSI STATUS ===")

    for (course in courses) {
        println("${course.displayInfo()} -> ${describe(course.status)}")
    }


    
    println("=== KEAHLIAN ===")

    val skills = mutableSetOf("Kotlin", "Java")

    skills.add("Python")
    skills.add("Kotlin")

    println("Skills : $skills")
    println("Jumlah : ${skills.size}")

    println("Apakah Swift ada? ${"Swift" in skills}")
    println("Apakah Python ada? ${"Python" in skills}")


    println("=== NILAI MAHASISWA ===")

    val scores = mutableMapOf<Int, Int>(
        101 to 80,
        102 to 90,
        103 to 75
    )

    
    scores[101] = 85

    
    scores.remove(103)

 
    for ((nim, score) in scores) {
        println("NIM: $nim, Nilai: $score")
    }

    println("Nilai NIM 999: ${scores[999]}")


   
    println("=== ADD COURSE ===")

    println(
        courses.addCourse(
            Course("PAB105", "PAB", CourseStatus.ACTIVE)
        )
    )

    println(
        courses.addCourse(
            Course("IF101", "Logpro", CourseStatus.ACTIVE)
        )
    )

    for (course in courses) {
        println(course.displayInfo())
    }
}