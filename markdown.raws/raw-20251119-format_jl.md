using Dates

# Change this to the directory you want to process
folder = @__DIR__


# Simple sanitization function
function sanitize(name::String)
    # Replace anything not A–Z, a–z, 0–9 with "_"
    s = replace(name, r"[^A-Za-z0-9]" => "_")

    # Collapse multiple underscores
    s = replace(s, r"_+" => "_")

    # Remove leading/trailing underscores if any
    s = strip(s, '_')

    return s
end

for oldname in readdir(folder)
    oldpath = joinpath(folder, oldname)

    # Skip directories
    isfile(oldpath) || continue

    # Get modification time
    mtime = unix2datetime(stat(oldpath).mtime)
    date_str = Dates.format(mtime, "yyyymmdd")

    # New filename
    newname = replace(oldname, r".md$" => "")
    newname = sanitize(newname)
    newname = "raw-$date_str-$newname.md"
    newpath = joinpath(folder, newname)

    # Rename the oldname unless it already has the prefix
    if !startswith(oldname, "raw-")
        @info("Renaming", oldname , newname)
        mv(oldpath, newpath)
    else
        println("Skipping $oldname (already renamed)")
    end
end
